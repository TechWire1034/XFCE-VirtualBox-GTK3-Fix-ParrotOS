# XFCE VirtualBox GTK3 Fix for Parrot OS: Solving "Failed to load module 'xapp-gtk3-module'"

## Overview
This guide documents how to resolve the `Gtk-Message: Failed to load module "xapp-gtk3-module"` error when launching the VirtualBox 7.1.8 GUI on Parrot OS 6.x with XFCE.  
The error occurs because VirtualBox’s Qt-based GUI attempts to load the xapp-gtk3-module for desktop integration in XFCE, but this module is missing in Parrot OS’s repositories (based on Debian Bullseye).  
The solution involves installing libxapp-gtk3-module from Debian Sid and verifying the setup in XFCE.

## Environment
- **Operating System**: Parrot OS 6.x (Lory), based on Debian Bullseye
- **Desktop Environment**: XFCE
- **VirtualBox Version**: 7.1.8 (build 168469)
- **Kernel**: 6.12.12-amd64

## Problem Description
When running `virtualbox` or `virtualbox --style Fusion` on Parrot OS with XFCE, the following error appears, and the GUI fails to launch:  

Gtk-Message: Failed to load module "xapp-gtk3-module"


## Cause
- The xapp-gtk3-module is part of the XApps project (developed by Linux Mint) and enhances GTK3 application integration in XFCE.
- Parrot OS’s repositories (Debian Bullseye, Parrot OS, Oracle VirtualBox) do not include xapp or libxapp-gtk3-module.
- VirtualBox’s GUI expects this module for proper rendering in XFCE, leading to the error.

## Steps to Reproduce
1. Install VirtualBox 7.1.8 on Parrot OS with XFCE.
2. Launch VirtualBox via terminal with `virtualbox` or `virtualbox --style Fusion`.
3. Observe the Gtk-Message error in XFCE.

## Solution
1. **Install `libxapp-gtk3-module` manually from Debian Sid**  
   - Add the Debian Sid repository (use caution due to potential instability):  
     ```bash
     echo "deb http://deb.debian.org/debian sid main" | sudo tee -a /etc/apt/sources.list
     ```
   - Update package lists and install the module for XFCE:  
     ```bash
     sudo apt update
     sudo apt install libxapp-gtk3-module
     ```
   - (Optional) Remove Sid to avoid conflicts: edit `/etc/apt/sources.list` and delete the added line.

2. **Test VirtualBox GUI launch in XFCE**  
   - Run VirtualBox:  
     ```bash
     virtualbox
     ```
   - Verify the GUI launches without the error in XFCE.

## Notes
- This fix is tailored for Parrot OS 6.x with XFCE and VirtualBox 7.1.8. It may work on Debian-based systems with XFCE but requires adaptation for other OSes (e.g., Fedora, Arch) or desktop environments.
- Use Debian Sid cautiously; consider pinning the package or finding a safer source for XFCE compatibility.
- Test after each step to ensure stability in XFCE.
