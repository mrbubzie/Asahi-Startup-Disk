# Asahi Startup Disk — 2.1-Final

<img width="2559" height="1585" alt="Screenshot_20261117_200612" src="https://github.com/user-attachments/assets/7e518762-c576-4f71-8253-2aa79e2bcc31" />

## Install

Requires Rust/Cargo, GTK4 development libraries, pkg-config, Python 3, polkit/pkexec, a graphical polkit authentication agent, and sudo. Run as your normal user:

## Recent Changes 2.1-Final
- General fixes and a brand new KDE Plasmamoid widget for quick access on the taskbar(optional) and can be refused during install.

<img width="942" height="806" alt="Screenshot_20261118_210519" src="https://github.com/user-attachments/assets/33498c89-3200-4bc3-b860-3a2692a7151e" />


```bash
unzip Asahi-Startup-Disk-2.1-final.zip
cd Asahi-Startup-Disk-2.1-final
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


## Credits

Uses the `asahi-bless` Rust crate and builds on earlier Asahi startup disk concepts. The original GNOME Startup Disk project is by Davide Cavalca: https://gitlab.gnome.org/davide125/startup-disk.
