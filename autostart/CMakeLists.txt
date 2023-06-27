#file(GLOB DESKTOP_FILES_IN *.desktop.in)

install(FILES
    lxqt-panelloader.desktop
    DESTINATION "${LXQT_ETC_XDG_DIR}/autostart"
    COMPONENT Runtime
)
