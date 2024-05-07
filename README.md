# lxqt-labwc-session

>Files for an LXQt 2.0 wayland session using the labwc compositor.


**Note**:

* The updated version uses the default labwc settings location now, if updating consider moving your settings to `~/.config/labwc.`

* `lxqt-panel 2.0 does not include yet the taskbar-plugin (aka window list) for wayland.
Manual installation is possible and recommended compiling from [Github](https://github.com/LXQt-Marcus-Fork/lxqt-panel/tree/wlroots-taskbar) directly or using [this PKGBUILD](https://github.com/stefonarch/LXQt-Wayland-files/tree/main/AUR/lxqt-panel).

Alternatively  sfwbar, waybar or yatbfw can be used to provide a taskbar, see `~/.config/labwc/autostart`.

Use your display manager to start "LXQt Labwc".
`startlxqtlabwc` directly from tty works too.

## Screenshots

![LXQt-labwc dark](labwc-dark.png)

* LXQt style: "Valendas"
* labwc: "Vent-dark" theme


![LXQt-labwc dark](Labwc.png)

* LXQt and Labwc style: "Clearlooks"

## Dependencies

Build dependencies are `CMake`, [lxqt] 2.0>= and optionally
`Git` to pull latest VCS checkouts. [labwc] version 0.7.1 or higher is recommended.

### Optional:

* swaybg, swaylock, swayidle for screen locking and background.

## Installation

Code configuration is handled by CMake.<br>
CMake variable `CMAKE_INSTALL_PREFIX` has to be set to `/usr` on most operating systems.

```
git clone https://github.com/stefonarch/lxqt-labwc-session.git
cd lxqt-labwc-session
mkdir build && cd build
cmake ..  -DCMAKE_INSTALL_PREFIX=/usr  -DCMAKE_BUILD_TYPE=Debug && make -j4

# Prefer creating a package for your distro instead of using sudo make install

```

## Changes in version 0.2

* With LXQt 2.0 no different location for labwc configuration is used anymore.
All LXQt components can be configured in "Configuration Center" with some exceptions,
see "Notes" below. Labwc configuration is handled in `~/.config/labwc` and panel position settings by
right click.

* Virtualized systems should be autodetected (fixing "no cursor" issue)

* F12 as toggledropdown shortcut for QTerminal is working (using the shipped configuration).

* Improved wallpaper.

## Packages:

For Arch based distributions an [AUR] package is available.


## Notes and Issues

* Default configuration is in `/usr/share/lxqt/wayland/labwc` and copied at first run
if labwc was never configured. Refer to those files if you have already configured labwc.

* LXQt lock settings do not work yet. For screenlock settings under wayland
 please check `~/.config/labwc/autostart`.

* Global shortcuts are handled exclusively in `~/.config/labwc/rc.xml`.

* Use `-/.config/labwc/autostart` to autostart wayland-only applications.

* Mouse cursor and size are synced and can be set using "Appearance" settings,
labwc restart required (`labwc -r` or ctrl-shift-R if  using the shipped configuration).
GTK settings have to be updated after changes.

* Bottom and right panels have some alignment issues for tooltips and and menu popups.

* Some X11-only applications (example: redshift) in autostart
can lead to high CPU usage under wayland.

* LXQt Mouse/touchpad and keyboard settings do not work but keyboard layout(s)
  will be imported and set at startup. See `~/.config/labwc/environment` and the
 "libinput" section in `rc.xml`.

* [Credit] for the original Vent theme

Support: matrix channel [#lxqt-labwc:matrix.org]


[AUR]:                    https://aur.archlinux.org/packages/lxqt-labwc-session-git
[labwc]:                  https://github.com/labwc/labwc/
[lxqt-session]:           https://github.com/lxqt/lxqt/
[sfwbar]:                 https://github.com/LBCrion/sfwbar
[yatbfw]:                 https://github.com/selairi/yatbfw/
[waybar]:                 https://github.com/Alexays/Waybar/
[Credit]:                 https://github.com/addy-dclxvi/openbox-theme-collections
[#lxqt-labwc:matrix.org]: https://matrix.to/#/#lxqt-labwc:matrix.org
