# 学习笔记仓库

主要记录技术学习笔记和经验总结，内容覆盖网络安全、性能优化、开发技术与学习资源四个方向。

## 目录结构

```text
.
├── README.md                  # 本文件：项目说明与文档索引
├── 01-网络安全/                # DDoS 攻防、协议工具、安全环境
├── 02-性能优化/                # 性能方法论、profiling 工具、实战案例
├── 03-开发技术/                # Git 工作流、Java 示例、服务器配置
└── 04-学习资源/                # 机器学习资料、大模型实践、常用工具收藏
```

## 文档索引

### 01-网络安全

| 文档 | 说明 |
| ---- | ---- |
| [DDoS 攻击防御原理](./01-网络安全/DDoS攻击防御原理.md) | HTTP 慢速连接、DNS 放大反射、DNS 缓存投毒、HTTP GET 攻击的原理与防御思路 |
| [DDoS 防御性能优化小结](./02-性能优化/DDoS防御性能优化小结.md) | DDoS 防御产品报文处理场景的性能优化实战（归档于性能优化分类） |
| [scapy 学习笔记](./01-网络安全/scapy学习笔记.md) | Scapy 报文构造库的安装与基础用法（发送 ICMP、解析响应） |
| [Windows10 子系统安装 KaliLinux](./01-网络安全/Windows10子系统安装KaliLinux.md) | 通过 WSL 在 Windows 10 中安装 Kali Linux 的步骤与限制 |

### 02-性能优化

| 文档 | 说明 |
| ---- | ---- |
| [性能优化记录](./02-性能优化/性能优化记录.md) | 性能优化方法框架：瓶颈定位与架构/硬件/流程/算法/代码/编译各层要点 |
| [DDoS 防御性能优化小结](./02-性能优化/DDoS防御性能优化小结.md) | 流程、算法、语句、编译四方面优化的实战总结（2012） |
| [Linux perf 学习笔记](./02-性能优化/Linux_perf学习笔记.md) | perf 性能分析工具的参考资源、事件图与常用命令速记 |

### 03-开发技术

| 文档 | 说明 |
| ---- | ---- |
| [GitHub 本地使用指南](./03-开发技术/GitHub本地使用指南.md) | Windows 下 Git + TortoiseGit + SSH 密钥配置与克隆流程 |
| [Java Telnet 客户端开发示例](./03-开发技术/Java_Telnet客户端开发示例.md) | Apache Commons Net TelnetClient 完整示例与 SSH（jsch）思路 |
| [阿里云 ECS Ubuntu 桌面环境配置](./03-开发技术/阿里云ECS_Ubuntu桌面环境配置.md) | ECS 安装 ubuntu-desktop、LightDM 配置与 .profile 报错修复 |

### 04-学习资源

| 文档 | 说明 |
| ---- | ---- |
| [机器学习入门资源](./04-学习资源/机器学习入门资源.md) | 《Machine Learning in Action》电子书、源码与学习路线 |
| [大模型学习](./04-学习资源/大模型学习.ipynb) | Colab 实验笔记本（持续更新中） |
| [常用工具与链接](./04-学习资源/常用工具与链接.md) | 图床、办公软件、系统/网络工具、学习站点收藏 |

## 书籍收藏

- [深入理解计算机系统（第三版）](http://eol.bnuz.edu.cn/meol/common/script/preview/download_preview.jsp?fileid=2169600&resid=242120&lid=28605)
- [Computer Systems: A Programmer's Perspective, 3rd ed.](https://github.com/smellslikekeenspirit/an-askreddit-list-of-compsci-books/blob/master/Randal%20E.%20Bryant%2C%20David%20R.%20O%E2%80%99Hallaron%20-%20Computer%20Systems.%20A%20Programmer%E2%80%99s%20Perspective%20%5B3rd%20ed.%5D%20(2016%2C%20Pearson).pdf)

## 维护约定

- 新增笔记按主题放入对应编号目录，文件名使用中文短横线分隔或英文小写下划线。
- 技术文档建议包含：标题、概述、正文（带代码块语言标注）、参考链接。
- 大体积文件（PDF、图片等）通过外链引用，存入仓库会显著增大克隆体积。
- 引用仓库内其他文档时使用相对路径，保证在 GitHub/IDE 中均可跳转。
