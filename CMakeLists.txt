cmake_minimum_required(VERSION 3.5.0 FATAL_ERROR)
project(lxqt-labwc-session)

list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/cmake")

include(GNUInstallDirs)

set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTOUIC ON)
set(CMAKE_INCLUDE_CURRENT_DIR ON)
set(CMAKE_POSITION_INDEPENDENT_CODE ON)

# Minimum Versions
set(LXQT_MINIMUM_VERSION "2.0.0")

find_package(lxqt ${LXQT_MINIMUM_VERSION} REQUIRED)
#find_package(Labwc REQUIRED)

find_package(PkgConfig REQUIRED)

# Please don't move, must be after lxqt
#find_package(XdgUserDirs REQUIRED)

# Patch Version
set(LXQT_LABWC_SESSION_PATCH_VERSION 0)

set(LXQT_LABWC_SESSION_VERSION 0.2)
add_definitions(
    "-DLXQT_LABWC_SESSION_VERSION=\"${LXQT_LABWC_SESSION_VERSION}\""
)

include(LXQtPreventInSourceBuilds)
include(LXQtCompilerSettings NO_POLICY_SCOPE)
include(GNUInstallDirs)
include(LXQtConfigVars)
file(GLOB DESKTOP_FILES_IN *.desktop.in)

find_program(LABWC_EXECUTABLE labwc)

if(LABWC_EXECUTABLE)
    execute_process(
        COMMAND ${LABWC_EXECUTABLE} --version
        OUTPUT_VARIABLE LABWC_VERSION
        OUTPUT_STRIP_TRAILING_WHITESPACE
    )
    message("Found labwc version: ${LABWC_VERSION}")
endif()


# startlxqt<compositor> scripts
set(PREDEF_XDG_DATA_DIRS "$XDG_DATA_HOME")
if(NOT("${LXQT_DATA_DIR}" MATCHES "^/usr(/local)?/share$"))
    set(PREDEF_XDG_DATA_DIRS "${PREDEF_XDG_DATA_DIRS}:${LXQT_DATA_DIR}")
endif()
set(PREDEF_XDG_DATA_DIRS "${PREDEF_XDG_DATA_DIRS}:/usr/local/share:/usr/share")
set(PREDEF_XDG_CONFIG_DIRS "/etc:${LXQT_ETC_XDG_DIR}:/usr/share")
#configure_file(toggledropdown.in toggledropdown @ONLY)
configure_file(startlxqtlabwc.in startlxqtlabwc @ONLY)
configure_file(lxqt-settingsexporter.in lxqt-settingsexporter @ONLY)

install(PROGRAMS
    "${CMAKE_CURRENT_BINARY_DIR}/startlxqtlabwc"
    "${CMAKE_CURRENT_BINARY_DIR}/lxqt-settingsexporter"
    DESTINATION "${CMAKE_INSTALL_BINDIR}"
    COMPONENT Runtime
)

install(FILES
    startlxqtlabwc.1
    DESTINATION "${CMAKE_INSTALL_MANDIR}/man1"
    COMPONENT Runtime
)

install(FILES
    lxqt-labwc.png
    DESTINATION "${LXQT_SHARE_DIR}/graphics"
    COMPONENT Runtime
)

install(FILES
    lxqt-labwc.desktop
    DESTINATION "${CMAKE_INSTALL_DATADIR}/wayland-sessions"
    COMPONENT Runtime
)

# default config files for compositors
add_subdirectory(config)

# wallpaper
add_subdirectory(wallpaper)

# openbox themes
add_subdirectory(themes)

