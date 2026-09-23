# Libra

Libra is a local-first AI agent for desktop use.

[English](./README.md) | [简体中文](./README.zh-CN.md)

## macOS (Apple Silicon)

Download the latest [dmg](https://dl.greenbit.ai/releases/latest/libra-desktop-aarch64.dmg), open it, and drag Libra to Applications. To upgrade, quit Libra and replace the existing app when prompted. You do not need to uninstall the old version separately.

## Windows (x86_64)

Download the latest [exe](https://dl.greenbit.ai/releases/latest/libra-desktop-x86_64.exe) and run the installer.

## Linux (Debian/Ubuntu)

If upgrading from 0.14.x to 1.0.0 or later, quit the old Libra app, run `sudo dpkg -r libra` to remove the old package, and follow the FAQ below to ensure its processes have exited before installing the new package.

Download the package for your architecture, then run its install command from the download directory:

- **ARM64:** [deb](https://dl.greenbit.ai/releases/latest/libra-desktop-aarch64.deb) — `sudo apt install ./libra-desktop-aarch64.deb`
- **x86_64:** [deb](https://dl.greenbit.ai/releases/latest/libra-desktop-x86_64.deb) — `sudo apt install ./libra-desktop-x86_64.deb`

APT will try to install the package dependencies `libwebkit2gtk-4.1-0` and `libgtk-3-0` from your configured repositories.

Launch Libra from the applications menu. If its launcher still shows outdated information after an upgrade, sign out and back in. To uninstall the Linux package, run `sudo dpkg -r libra`.

### FAQ: old Libra processes remain

Close the old Libra app first. If `manager.bin` or `gbx_lm.bin` from `/opt/Libra` is still running, stop those processes:

```sh
sudo pkill -TERM -f '^/opt/Libra/resources/bin/(manager\.bin|gbx_lm\.bin)([[:space:]]|$)'
```

After a few seconds, check for remaining processes:

```sh
sudo pgrep -af '^/opt/Libra/resources/bin/(manager\.bin|gbx_lm\.bin)([[:space:]]|$)'
```

If any remain, force them to exit:

```sh
sudo pkill -KILL -f '^/opt/Libra/resources/bin/(manager\.bin|gbx_lm\.bin)([[:space:]]|$)'
```
