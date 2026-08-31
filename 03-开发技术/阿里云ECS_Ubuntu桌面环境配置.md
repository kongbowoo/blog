# 阿里云 ECS Ubuntu 桌面环境配置

> 概述：阿里云 ECS 默认安装的是无桌面的 Ubuntu Server。本文记录在 ECS 实例上安装 Ubuntu 桌面环境，并配置 LightDM 登录、修复 `.profile` 报错的过程。

## 安装桌面环境

Ubuntu Server 默认无图形界面，先安装桌面组件：

```shell
apt-get update
apt-get install ubuntu-desktop
```

安装完成后需要重启系统。

## 配置 LightDM 登录

安装后进入 LightDM 配置目录并编辑配置文件：

```shell
cd /usr/share/lightdm/lightdm.conf.d/
vim 50-ubuntu.conf
```

在文件中增加如下配置（允许手动输入用户名登录、禁用访客会话）：

```ini
[Seat:*]
user-session=ubuntu
greeter-show-manual-login=true
allow-guest=false
```

> 注：原笔记中写作 `allow-guest-false`，LightDM 的正确语法为 `allow-guest=false`，此处已修正。

## 修复登录时的 .profile 报错

以 root 登录桌面后，终端可能提示 `mesg: ttyname failed: Inappropriate ioctl for device`。原因在于 `/root/.profile` 中的 `mesg n` 在非 tty 环境下执行失败。

编辑 `/root/.profile`：

```shell
vim /root/.profile
```

原内容：

```shell
# ~/.profile: executed by Bourne-compatible login shells.

if [ "$BASH" ]; then
  if [ -f ~/.bashrc ]; then
    . ~/.bashrc
  fi
fi

mesg n || true
```

将最后一行 `mesg n || true` 修改为：

```shell
tty -s && mesg n || true
```

修改后重新登录即可生效。
