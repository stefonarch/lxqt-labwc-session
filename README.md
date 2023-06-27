# lxqt-wayland-session

Files for a LXQt wayland session using the labwc compositor. Settings for waybar's wlr/taskbar and [yatbfw]() panel are also provided.

Use your display manager to start the session. Starting `startlxqtlabwc` from tty should work too.

## Requisites

* LXQt version 1.3
* [labwc-git](https://github.com/labwc/labwc)
* [lxqt-notificationd-wip]()

## Installation

Build dependencies are CMake, [lxqt-session](https://github.com/lxqt/lxqt-session) and optionally Git to pull latest VCS checkouts.

```
git clone https://github.com/lxqt/stefonarch/lxqt-labwc-session
cd lxqt-labwc-session
mkdir build && cd build/
cmake ..  -DCMAKE_INSTALL_PREFIX=/usr
make
sudo make install
```

## Notes

* In `session settings` uncheck "lxqt-panel" module and check "lxqt-panelloader" in order to use different settings
for the lxqt-panel on wayland.
* Don't use bottom positions for notifications (multiple notifications are going out of screen).
* Shortcuts are handled exclusively in `~/.config/lxqt-wayland/labwc/rc.xml`
* Some panel plugins do not work on wayland, see [lxqt-panel]().



