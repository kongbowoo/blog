# GitHub 本地使用指南

> 概述：在 Windows 环境下配置 Git 并连接 GitHub 的基本流程：安装 Git 与 TortoiseGit 客户端、生成 SSH 密钥对、在 GitHub 添加公钥、克隆代码。

## 安装 Git

- Git for Windows 下载地址：<https://git-for-windows.github.io/>

## 安装 TortoiseGit 客户端

- TortoiseGit 下载地址：<https://tortoisegit.org/download/>

## 本地生成公钥和私钥

- 使用 TortoiseGit 安装目录下的 PuTTYgen 工具生成公钥和私钥。

![PuTTYgen 生成密钥](https://i.loli.net/2018/03/10/5aa3e7f946f7a.png)

- 点击 Save private key 将私钥保存到本地（`.ppk` 文件），公钥内容留在剪贴板/文本中待用。

## 在 GitHub 上添加公钥

- 打开 GitHub -> Settings -> SSH and GPG keys -> New SSH key，将公钥内容粘贴进去。

![GitHub 添加公钥](https://i.loli.net/2018/03/10/5aa3e7f95604a.png)

## 克隆代码

- 使用 TortoiseGit 的 Clone 菜单，填写仓库地址，指定加载本地私钥，即可克隆代码到本地。

![TortoiseGit 克隆代码](https://i.loli.net/2018/03/10/5aa3ec2a034ad.png)

## 注意

- 文中截图托管于第三方图床（i.loli.net），如失效可按上述文字步骤操作。
