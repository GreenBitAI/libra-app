# Libra

Libra 是面向桌面使用的端侧优先 AI Agent。

[English](./README.md) | [简体中文](./README.zh-CN.md)

## macOS（Apple 芯片）

下载最新的 [dmg](https://dl.greenbit.ai/releases/latest/libra-desktop-aarch64.dmg)，打开后将 Libra 拖入“应用程序”。升级时先退出 Libra，复制新版应用并在提示时选择替换，无需单独卸载旧版。

## Windows（x86_64）

下载最新的 [exe](https://dl.greenbit.ai/releases/latest/libra-desktop-x86_64.exe)，运行安装程序。

## Linux（Debian/Ubuntu）

从 0.14.x 升级至 1.0.0 或更新版本时，先退出旧版 Libra，运行 `sudo dpkg -r libra` 卸载旧包，再按下方 FAQ 确认旧进程已退出，然后安装新版。

下载对应架构的安装包，在终端进入下载目录后运行：

- **ARM64：** [deb](https://dl.greenbit.ai/releases/latest/libra-desktop-aarch64.deb) — `sudo apt install ./libra-desktop-aarch64.deb`
- **x86_64：** [deb](https://dl.greenbit.ai/releases/latest/libra-desktop-x86_64.deb) — `sudo apt install ./libra-desktop-x86_64.deb`

`apt` 会尝试从已配置的软件源补齐安装包依赖的 `libwebkit2gtk-4.1-0` 和 `libgtk-3-0`。

安装后从应用菜单启动 Libra。如果升级后启动项仍显示旧信息，退出桌面会话并重新登录。卸载 Linux 安装包可运行 `sudo dpkg -r libra`。

### FAQ：旧版 Libra 进程仍在运行

先退出旧版 Libra。如果 `/opt/Libra` 下的 `manager.bin` 或 `gbx_lm.bin` 仍在运行，执行：

```sh
sudo pkill -TERM -f '^/opt/Libra/resources/bin/(manager\.bin|gbx_lm\.bin)([[:space:]]|$)'
```

等待几秒后检查是否还有残留进程：

```sh
sudo pgrep -af '^/opt/Libra/resources/bin/(manager\.bin|gbx_lm\.bin)([[:space:]]|$)'
```

如果仍有输出，再强制结束：

```sh
sudo pkill -KILL -f '^/opt/Libra/resources/bin/(manager\.bin|gbx_lm\.bin)([[:space:]]|$)'
```
