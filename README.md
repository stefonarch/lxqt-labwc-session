# lxqt-labwc-session

Files for an experimental LXQt wayland session using the labwc compositor.<br>
Settings for [waybar] or [yatbfw] taskbars are also provided.<br>
*Should* not interfere with existing LXQt X11 sessions.

Use your display manager to start the session.
`startlxqtlabwc` from tty should work too.

## Dependencies

* `LXQt` version 1.3
* `labwc` 0.6.4 or [labwc-git]
* [waybar] (default) or [yatbfw] (needed as taskmanager)
* [lxqt-notificationd-wip] for better experience with `lxqt-notificationd` (optional)
* [lxqt-wlogout] for complete logout closing lxqt-session first (optional)
* swaybg, swaylock, swayidle for screen locking and background (optional)

Build dependencies are `CMake`, [lxqt-session] and optionally
`Git` to pull latest VCS checkouts.

## Installation

Code configuration is handled by CMake.<br>
CMake variable `CMAKE_INSTALL_PREFIX` has to be set to `/usr` on most operating systems.

```bash
git clone https://github.com/stefonarch/lxqt-labwc-session.git
cd lxqt-labwc-session
mkdir build && cd build
cmake -D CMAKE_BUILD_TYPE=Release -D CMAKE_INSTALL_PREFIX=/usr
cmake --build build --config Release

# Use your distro package manager instead using sudo make install
DESTDIR="$(pwd)/package" cmake --build build --target install
```

## Packages:

For Arch based distributions an [AUR] package is available.

## Notes

* In "Session Settings" **uncheck** the "Panel" module and check only
  "Panel X11/Wayland" in order to use different settings for `lxqt-panel`
  on wayland. Panels with a "Desktop switch" widget will crash - do not add it.
* LXQt lock settings do not work yet. For screenlock settings under wayland
  please check `~/.config/lxqt-wayland/labwc/autostart`.
* **Update**: To hide the panel with fullscreen applications use `<action name="ToggleAlwaysOnBottom"/>` in `~/.config/lxqt-wayland/labwc/rc.xml` "Windowrules" section
* Some X11-only applications (example: redshift) in autostart
  can lead to high CPU usage under wayland.
* All options for labwc with LXQt are handled in `~/.config/lxqt-wayland/labwc/`.
* LXQt Mouse/touchpad and keyboard settings do not work but keyboard layout(s)
  should be imported or set at first run. See
  `~/.config/lxqt-wayland/labwc/environment` and the "libinput" section in `rc.xml`.
* Global shortcuts are handled exclusively in `~/.config/lxqt-wayland/labwc/rc.xml`.
* Refer also to this file for some lxqt-settings (e.g. positions)
* Some panel plugins do not work on wayland, see [lxqt-panel] for more information.


[AUR]:                    https://aur.archlinux.org/packages/lxqt-labwc-session-git
[labwc-git]:              https://github.com/labwc/labwc/
[lxqt-notificationd-wip]: https://github.com/stefonarch/lxqt-notificationd/tree/wip_layer_shell_qt/
[lxqt-panel]:             https://github.com/stefonarch/LXQt-Wayland-files/blob/main/lxqt-panel.md
[lxqt-session]:           https://github.com/lxqt/lxqt-session/
[yatbfw]:                 https://github.com/selairi/yatbfw/
[waybar]:                 https://github.com/Alexays/Waybar/
[lxqt-wlogout]:           https://github.com/stefonarch/lxqt-wlogout
