+++
title = "Night Light as redshift oneshot replacement under Gnome in Ubuntu 22.04"
date = 2022-08-06

[taxonomies]
tags = ["gnome", "night light", "redshift", "ubuntu", "wayland", "bash"]
+++

`redshift -O [VALUE]` has been an eye-saver for me on Ubuntu 20.04. Unfortunately it no longer works on a fresh Ubuntu 22.04 install.

<!-- more -->

Gnome comes with a Night Light feature out of the box, but I'm not a huge fan of automatic or time-based temperature adjustment. My sleep schedule and eye-soreness levels vary a fair amount so I prefer manual control (plus it's nice when switching between tasks that require different temps).

The Gnome settings UI is not ideal as it takes 3-4 clicks to open, only lets you adjust the temperature in range 1700-4700, and doesn't show the actual values.

{{ figure(src="/2022-08-06-wayland-redshift/night-light.png", caption="Night Light in Gnome") }}

You can, however, create a bash alias that controls the built in Night Light via `gsettings` to replace `redshift`'s oneshot feature:

```bash
# place in ~/.bash_aliases and 'source' the file
function red_shift() {
	gsettings set org.gnome.settings-daemon.plugins.color night-light-enabled true
	gsettings set org.gnome.settings-daemon.plugins.color night-light-schedule-automatic false
	gsettings set org.gnome.settings-daemon.plugins.color night-light-schedule-from 0.0
	gsettings set org.gnome.settings-daemon.plugins.color night-light-schedule-to 0.0
	gsettings set org.gnome.settings-daemon.plugins.color night-light-temperature $1
}
alias rs=red_shift
```

```bash
# usage: rs [VALUE] (6500 = default)
rs 2000
```