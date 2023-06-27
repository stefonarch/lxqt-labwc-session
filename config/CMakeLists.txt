# install default config files to /usr/share/lxqt/wayland
install(DIRECTORY
    labwc
    DESTINATION "${CMAKE_INSTALL_DATADIR}/lxqt/wayland"
    COMPONENT Runtime
)
install(FILES
    panel-wayland.conf
    DESTINATION "${CMAKE_INSTALL_DATADIR}/lxqt/wayland"
    COMPONENT Runtime
)
