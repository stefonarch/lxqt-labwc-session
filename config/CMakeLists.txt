# install default config files to /usr/share/lxqt/wayland
install(DIRECTORY
    labwc
    waybar
    DESTINATION "${CMAKE_INSTALL_DATADIR}/lxqt/wayland"
    COMPONENT Runtime
)
configure_file(panel-wayland.conf.in panel-wayland.conf @ONLY)
install(FILES
    "${CMAKE_CURRENT_BINARY_DIR}/panel-wayland.conf"
    yatbfw-taskbar.json
    DESTINATION "${CMAKE_INSTALL_DATADIR}/lxqt/wayland"
    COMPONENT Runtime
)
