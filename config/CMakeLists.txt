# install default config files to /usr/share/lxqt/wayland
install(DIRECTORY
    labwc
    DESTINATION "${CMAKE_INSTALL_DATADIR}/lxqt/wayland"
    COMPONENT Runtime
)
