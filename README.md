# lxqt-labwc-session

Files for a LXQt wayland session using the labwc compositor. Settings for waybar's wlr/taskbar and [yatbfw]() panel are also provided. Does not interfere with existing X11 LXQt sessions.

Use your display manager to start the session. `startlxqtlabwc` from tty should work too.

## Requisites

* LXQt version 1.3
* [labwc-git](https://github.com/labwc/labwc)
* waybar (default) or yatbfw (needed as taskmanager)
* [lxqt-notificationd-wip](https://github.com/stefonarch/lxqt-notificationd/tree/wip_layer_shell_qt) for better experience with `lxqt-notificationd` (optional)
* [lxqt-wlogout](https://github.com/stefonarch/lxqt-wlogout) for complete logout (optional)
* swaybg, swaylock, swayidle for screen locking and background (optional)



## Installation

Build dependencies are CMake, [lxqt-session](https://github.com/lxqt/lxqt-session) and optionally Git to pull latest VCS checkouts.

Code configuration is handled by CMake. CMake variable CMAKE_INSTALL_PREFIX has to be set to /usr on most operating systems.

To build run `make`, to install `make install` which accepts variable DESTDIR as usual.

## Packages:

For arch based distributions an [AUR]() packages is available.

## Notes

* In "Session Settings" uncheck the "Panel" module and check "Panel X11/Wayland" in order to use different settings
for `lxqt-panel` on wayland. Panels with a "Desktop switch" widget will crash - so do not add it.
* Some X11-only applications (example: redshift) in autostart can lead to high CPU usage under wayland.
* Options for labwc are handled in `~/.config/lxqt-wayland/labwc/`.
* Don't use bottom positions for notifications (multiple notifications will go out of screen).
* Global shortcuts are handled exclusively in `~/.config/lxqt-wayland/labwc/rc.xml`.
* Some panel plugins do not work on wayland, see [lxqt-panel](https://github.com/stefonarch/LXQt-Wayland-files/blob/main/lxqt-panel.md) for more information.



