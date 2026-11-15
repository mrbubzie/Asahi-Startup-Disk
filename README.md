
# Asahi Startup Disk v1.4.3 — KDE Plasma Edition
<img width="2201" height="1481" alt="Screenshot_20261115_180229" src="https://github.com/user-attachments/assets/5ff8d7b3-60d1-4ed7-8868-6d3b4947d95b" />
**Developer:** Ryan  
**Platform:** Apple Silicon Macs running Asahi Linux  
**Status:** Experimental release — boot-selection functionality has not yet been hardware-validated.

![Asahi Startup Disk interface photos](asahi-startup-disk-interface-preview.png)

*Interface photos from development builds, supplied by the developer. Version 1.4.3 includes further title and layout adjustments.*

## Overview

Asahi Startup Disk is a KDE-compatible Qt6 desktop application for viewing startup volumes and selecting the operating system used to boot an Apple Silicon Mac running Asahi Linux. It uses a Rust helper built around `asahi-bless` for boot selection.

### Features

- Display available startup volumes, including detected macOS and Linux entries.
- Select a **default startup disk** or choose **Boot Once** for the next startup.
- Show detected Mac hardware details from the Linux device tree, with a generic fallback for unrecognized models.
- Dark, blue-accented KDE Plasma interface, bundled drive icons and custom blue hard-drive application icon.
- Polkit authentication for privileged actions; no automatic reboot.
- Includes `install.sh` and `uninstall.sh`.

## Requirements

- An **Apple Silicon Mac** running a compatible **Asahi Linux** installation with the expected NVRAM device (`/dev/mtd/by-name/nvram`) and working `asahi-bless` support.
- **Python 3** and **PySide6 (Qt6)** for the graphical interface.
- **Rust and Cargo** to compile the helper at install time.
- **Polkit**, `pkexec`, and a graphical Polkit authentication agent.
- **sudo** for system-wide installation.
- KDE Plasma 6 recommended. The Qt Widgets frontend is **not** a Kirigami/QML application.
- Internet access for Cargo dependencies on a first build, unless already cached.

### Gentoo

```bash
sudo emerge --ask dev-lang/rust dev-python/pyside6 sys-auth/polkit
```

Confirm that `pkexec`, `sudo`, and a graphical Polkit authentication agent are available in your desktop session. Package names, USE flags, and availability can vary by Gentoo profile.

### Arch Linux / Arch Linux ARM

```bash
sudo pacman -S --needed rust python-pyside6 polkit sudo
```

Ensure a graphical Polkit authentication agent is running.

## Installation

Download `asahi-startup-disk-plasma-v1.4.3-final.zip` from the release assets, then:

```bash
unzip Asahi-Startup-Disk-v1.4.3-final.zip
cd Asahi-Startup-Disk-v1.4.3-final
./install.sh
```

Launch **Asahi Startup Disk** from the KDE application menu, or run:

```bash
plasma-startup-disk
```

If the launcher icon remains cached:

```bash
kbuildsycoca6 --noincremental
```

If you pinned an older launcher, unpin and pin the updated application again.

## Uninstallation

From the extracted project directory:

```bash
./uninstall.sh
```

Confirm the removal prompt. The script removes application-installed files while preserving shared system dependencies and boot settings. Keep the extracted project directory if you may need to uninstall later.

## Changes in v1.4.3

- Adjusted the sidebar so **Asahi Startup Disk** appears on one line.
- Refined typography, card spacing, navigation focus, and visual balance.
- Corrected capitalization to **Asahi Linux** and **This Mac**.
- Retained the custom blue hard-drive icon.
- Updated About information to **Version 1.4.3** and **Developer: Ryan**.
- Kept the existing Rust boot-management logic unchanged.

## Important limitations and safety

**This build is not yet validated on real Apple Silicon hardware.** Python/Bash syntax and ZIP integrity checks do not establish successful Rust compilation, working Polkit authentication, or safe boot changes. Modifying Apple Silicon NVRAM incorrectly can prevent normal startup and may require recovery procedures. Do not test on a machine without a working recovery plan or while another NVRAM writer is running.

The application does not extract APFS volume icons, does not automatically reboot, and does not manage battery, thermal, charging, or fan settings.

## Credits

**Developer:** Ryan  
**Original project inspiration:** GNOME Startup Disk by Davide Cavalca (MIT-licensed original source).  
**Backend library:** `asahi-bless`.
