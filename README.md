# Asahi Startup Disk — 2.0 RC1

<img width="2560" height="1590" alt="Screenshot_20261116_202033" src="https://github.com/user-attachments/assets/262252df-0d62-4f50-b4ab-6ca6c5dff868" />

## Install

Requires Rust/Cargo, GTK4 development libraries, pkg-config, Python 3, polkit/pkexec, a graphical polkit authentication agent, and sudo. Run as your normal user:

```bash
unzip Asahi-Startup-Disk-2.0-RC1-final.zip
cd Asahi-Startup-Disk-2.0-RC1-final
chmod +x install.sh or uninstall.sh if you wish to uninstall
./install.sh or ./uninstall.sh
```

Launch **Asahi Startup Disk** from the KDE application menu, or run `asahi-startup-disk-rust`.

## One authentication per app session

On the first startup-disk scan, polkit prompts for administrator authorization. Once approved, a private authenticated helper remains alive while the application runs. Refresh, Set as Default, and Next Boot reuse the same helper without another prompt. No password is saved. Closing the app closes the helper's input pipe, causing it to exit. If authentication is cancelled or the helper terminates, retrying an operation starts a new authorization session.

Only `list`, `set-default`, and `set-next` commands are accepted; write operations re-check candidate UUIDs against currently detected boot volumes. The privileged helper does not listen on a network or local socket.

## Uninstall

```bash
./uninstall.sh
```

The uninstaller removes the installed application and bundled assets, not shared system dependencies.

## Safety and limitations

This is a release candidate, not hardware-verified software. Changing Apple Silicon boot settings can make a system unbootable. Keep a recovery path available. Do not run simultaneous NVRAM-changing utilities. The application does not automatically reboot, and the boot-picker option is informational only. OS identification is best-effort and may not identify unmounted installations.

## Credits

Uses the `asahi-bless` Rust crate and builds on earlier Asahi startup disk concepts. The original GNOME Startup Disk project is by Davide Cavalca: https://gitlab.gnome.org/davide125/startup-disk.
