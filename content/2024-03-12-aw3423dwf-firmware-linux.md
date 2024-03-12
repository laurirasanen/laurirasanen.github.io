+++
title = "Updating Alienware AW3423DWF firmware on Linux using a Windows 10 VM inside VirtualBox"
date = 2024-03-12

[taxonomies]
tags = ["linux", "firmware", "alienware", "aw3423dwf"]
+++

Alienware AW3423DWF support page only comes with a Windows executable for updating the monitor firmware. It does not seem to work with Wine currently, but it can be run using a Windows 10 VM inside VirtualBox.

<!-- more -->

## VirtualBox

This is not a tutorial for installing VirtualBox. See a relevant wiki for your distribution, e.g. [https://wiki.archlinux.org/title/VirtualBox](https://wiki.archlinux.org/title/VirtualBox) for Arch.

That being said, here are some pitfalls to avoid during the process:

- Make sure to add yourself to the `vboxusers` group. Otherise VirtualBox won't be able to access USB devices.
- Install the Guest Additions disc for easy file sharing from host. 
- Install the Oracle Extension Pack for better USB support.
- Make sure to use a USB 3.0 (or above) port. 2.0 did not work for me.

## Passing the monitor USB to the VM

You should have a working Windows 10 VM that you can copy files to at this point.

Connect the upstream USB-B from the monitor to your computer. Unplug any other USB passthrough devices plugged into the monitor.

Find the monitor identifier with `lsusb`.

{{ figure(src="/2024-03-12-aw3423dwf-firmware-linux/lsusb.png", caption="Alienware monitor in lsusb output") }}

In VirtualBox, go to the VM USB settings and enable and the USB 3.0 controller.

Add the monitor USB device to the filter list. Mine shows up as a Realtek HID device, just make sure the ID is the same as in `lsusb`.

{{ figure(src="/2024-03-12-aw3423dwf-firmware-linux/vb-usb1.png", caption="VirtualBox USB settings") }}

{{ figure(src="/2024-03-12-aw3423dwf-firmware-linux/vb-usb2.png", caption="The monitor in VirtualBox USB settings") }}

Run the firmware updater inside the VM.

If your monitor isn't detected, something is probably wrong with your VirtualBox USB setup.

{{ figure(src="/2024-03-12-aw3423dwf-firmware-linux/vb-install1.png", caption="The firmware update utility running inside the VM") }}

Updating will take a few minutes and the monitor will reboot at the end.

{{ figure(src="/2024-03-12-aw3423dwf-firmware-linux/vb-install2.png", caption="Completed firmware update inside the VM") }}

Profit.

{{ figure(src="/2024-03-12-aw3423dwf-firmware-linux/monitor-info.png", caption="AW3423DWF with up-to-date firmware") }}

