cmake_minimum_required(VERSION 3.1.0 FATAL_ERROR)
project(lxqt-labwc-session)

list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/cmake")

include(GNUInstallDirs)

set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTOUIC ON)
set(CMAKE_INCLUDE_CURRENT_DIR ON)
set(CMAKE_POSITION_INDEPENDENT_CODE ON)

# Minimum Versions
set(LXQT_MINIMUM_VERSION "1.3.0")

find_package(lxqt ${LXQT_MINIMUM_VERSION} REQUIRED)
#find_package(Labwc REQUIRED)

find_package(PkgConfig REQUIRED)

# Please don't move, must be after lxqt
find_package(XdgUserDirs REQUIRED)

# Patch Version
set(LXQT_LABWC_SESSION_PATCH_VERSION 0)

set(LXQT_WAYLAND_SESSION_VERSION 0.1)
add_definitions(
    "-DLXQT_LABWC_SESSION_VERSION=\"${LXQT_LABWC_SESSION_VERSION}\""
)

include(LXQtPreventInSourceBuilds)
include(LXQtCompilerSettings NO_POLICY_SCOPE)
include(GNUInstallDirs)

# merged from lxqt-common
include(LXQtConfigVars)
file(GLOB DESKTOP_FILES_IN *.desktop.in)

# startlxqt<compositor> scripts
set(PREDEF_XDG_DATA_DIRS "$XDG_DATA_HOME")
if(NOT("${LXQT_DATA_DIR}" MATCHES "^/usr(/local)?/share$"))
    set(PREDEF_XDG_DATA_DIRS "${PREDEF_XDG_DATA_DIRS}:${LXQT_DATA_DIR}")
endif()
set(PREDEF_XDG_DATA_DIRS "${PREDEF_XDG_DATA_DIRS}:/usr/local/share:/usr/share")
set(PREDEF_XDG_CONFIG_DIRS "/etc:${LXQT_ETC_XDG_DIR}:/usr/share")
configure_file(startlxqtlabwc.in startlxqtlabwc @ONLY)
configure_file(lxqt-panelloader.in lxqt-panelloader @ONLY)

install(PROGRAMS
    "${CMAKE_CURRENT_BINARY_DIR}/startlxqtlabwc"
    "${CMAKE_CURRENT_BINARY_DIR}/lxqt-panelloader"
    DESTINATION "${CMAKE_INSTALL_BINDIR}"
    COMPONENT Runtime
)

install(FILES
    startlxqtlabwc.1
    DESTINATION "${CMAKE_INSTALL_MANDIR}/man1"
    COMPONENT Runtime
)

# default config files for compositors
add_subdirectory(config)

# wayland *.desktop files for display managers
add_subdirectory(wayland-sessions)

# lxqt-module for lxqt-panelloader
add_subdirectory(autostart)

#install(DIRECTORY "wallpaper/" DESTINATION "${LXQT_GRAPHICS_DIR}")
#add_subdirectory(wallpaper)

