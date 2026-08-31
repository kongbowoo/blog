# Windows10 子系统安装 Kali Linux

> 概述：通过 Windows Subsystem for Linux（WSL），可以在 Windows 10 环境中直接运行 Kali Linux，无需虚拟机或双系统。适合快速搭建轻量的渗透测试/安全学习环境。

## 官方说明

- 发布公告：<https://www.kali.org/news/kali-linux-in-the-windows-app-store/>

## 安装步骤

1. 在 Windows 10 中启用"适用于 Linux 的 Windows 子系统"功能：
   - 以管理员身份打开 PowerShell，执行 `Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux`，或通过"控制面板 -> 程序和功能 -> 启用或关闭 Windows 功能"勾选。
2. 重启系统。
3. 在 Microsoft Store 中搜索"Kali Linux"并安装。
4. 安装完成后从开始菜单启动 Kali Linux，完成初始用户配置。

## 注意事项

- WSL 默认无图形界面，如需 Kali GUI 可安装 Win-KeX 或使用 X Server 转发。
- 部分依托内核模块的工具（如自定义驱动、aircrack-ng 无线注入）在 WSL 下功能受限，完整环境建议使用虚拟机或物理机。
