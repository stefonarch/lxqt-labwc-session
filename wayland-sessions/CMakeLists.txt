file(GLOB SESSION_FILES_IN *.desktop.in)

MACRO(INSTALL_SESSION_FILES directory)
    install(FILES
            ${SESSION_FILES}
            DESTINATION "${directory}"
            COMPONENT Runtime
    )
ENDMACRO(INSTALL_SESSION_FILES)

INSTALL_SESSION_FILES("${CMAKE_INSTALL_DATAROOTDIR}/wayland-sessions")

