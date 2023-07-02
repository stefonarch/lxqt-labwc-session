# install default config files to /usr/share/lxqt/wayland
install(DIRECTORY
    labwc
    waybar
    DESTINATION "${CMAKE_INSTALL_DATADIR}/lxqt/wayland"
    COMPONENT Runtime
)
install(FILES
    panel-wayland.conf
    yatbfw-taskbar.json
    DESTINATION "${CMAKE_INSTALL_DATADIR}/lxqt/wayland"
    COMPONENT Runtime
)
