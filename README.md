# XFCE VirtualBox GTK3 Module Fix for Parrot OS

## Issue

When running VirtualBox on **Parrot OS (XFCE)**, you may encounter the following message in the terminal:

Gtk-Message: Failed to load module "xapp-gtk3-module"


This message appears because the `xapp-gtk3-module` (commonly used for desktop integration features like theming and window controls) is not installed by default on Parrot OS, as it typically exists in Linux Mint and some other distributions.

## Cause

VirtualBox uses GTK3 for its user interface, and it tries to load optional modules like `xapp-gtk3-module` to integrate better with your desktop environment. Since Parrot OS is based on Debian and doesn’t include this module in its repositories, the system throws a harmless warning message.

## Fix

To resolve this, you can manually install the `libxapp-gtk3-module` package from the **Debian Sid (Unstable)** repository. This is a small, standalone package that won’t disrupt your system if installed carefully.

### Steps:

1. Download the latest `libxapp-gtk3-module` `.deb` package from [Debian Sid packages archive](https://packages.debian.org/sid/libxapp-gtk3-module).

    Example:
    ```bash
    wget http://ftp.de.debian.org/debian/pool/main/x/xapp/libxapp-gtk3-module_2.8.2-1_amd64.deb
    ```

2. Install the package using `dpkg`:
    ```bash
    sudo dpkg -i libxapp-gtk3-module_*.deb
    ```

3. Done. The warning message should no longer appear when launching VirtualBox.

## Important Notes

- This message is **harmless** and does not affect the functionality of VirtualBox. You can safely ignore it if you prefer.
- **No need to reinstall the VirtualBox Extension Pack** — it is unrelated to this issue.


