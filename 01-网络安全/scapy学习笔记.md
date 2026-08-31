# Scapy 学习笔记

> 概述：Scapy 是一个强大的 Python 网络报文构造、发送、嗅探与解析库，常用于协议实验与安全测试。本文记录 Windows 环境下 Scapy 的基本使用方法。

## Scapy 安装说明

```shell
# 安装 Scapy
pip install scapy

# 安装 Npcap（Windows 抓包驱动，安装时勾选 WinPcap API 兼容模式）
```

## Scapy 使用说明

> 参考文档：<http://blog.csdn.net/Al_xin/article/details/52305549>

打开命令行，输入 `python` 进入 Python 解释器，导入 Scapy：

```python
>>> import scapy.all as scapy
WARNING: No route found for IPv6 destination :: (no default route?). This affects only IPv6
```

如果出现以下信息，则说明运行正常：

```python
>>> scapy.IP()
<IP  |>
```

**注：Linux 下运行方式与 Windows 不一样，网上大部分文章以 Linux 进行说明；Windows 下调用接口需要加前缀 `scapy.`。**

> 在线文档：<http://scapy.readthedocs.io/en/latest/#starting-scapy>

## 发送报文

发送单个 ICMP 报文（不等待响应）：

```python
scapy.send(scapy.IP(dst="192.168.115.188") / scapy.ICMP())
```

发送并接收响应（`sr1` 返回第一个应答报文）：

```python
>>> p = scapy.sr1(scapy.IP(dst="192.168.1.1") / scapy.ICMP() / "test")
Begin emission:
Finished to send 1 packets.
*
Received 4 packets, got 1 answers, remaining 0 packets
```

查看响应报文内容：

```python
>>> p
<IP  version=4 ihl=5 tos=0x0 len=32 id=6083 flags= frag=0 ttl=64 proto=icmp chksum=0xdfbf src=192.168.1.1 dst=192.168.1.9 options=[] |<ICMP  type=echo-reply code=0 chksum=0x1826 id=0x0 seq=0x0 |<Raw  load='test' |>>>

>>> p.show()
###[ IP ]###
  version   = 4
  ihl       = 5
  tos       = 0x0
  len       = 32
  id        = 6083
  flags     =
  frag      = 0
  ttl       = 64
  proto     = icmp
  chksum    = 0xdfbf
  src       = 192.168.1.1
  dst       = 192.168.1.9
  \options   \
###[ ICMP ]###
     type      = echo-reply
     code      = 0
     chksum    = 0x1826
     id        = 0x0
     seq       = 0x0
###[ Raw ]###
        load      = 'test'
```

## 相关笔记

- [DDoS 攻击防御原理](./DDoS攻击防御原理.md)：Scapy 常用于构造探测报文验证防御规则。
