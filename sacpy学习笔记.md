# Scapy学习笔记

python scapy DDoS

---
# Scapy安装说明

# Scapy使用说明
> 参考文档：http://blog.csdn.net/Al_xin/article/details/52305549

打开命令行，输入Python进入Python解释器
输入import scapy.all as scapy 

```python
>>>import scapy.all as scapy
WARNING: No route found for IPv6 destination :: (no default route?). This affects only IPv6
```

如果出现以下信息，则说明运行正常。
```python
>>>scapy.IP()
<IP  |>
```

**注：linux下运行方式与windows不一样，网上大部分文章是以linux进行说明的。**

> 在线文档：http://scapy.readthedocs.io/en/latest/#starting-scapy

发送报文

scapy.send(scapy.IP(dst="192.168.115.188")/scapy.ICMP())

**注：windows下运行需要加前缀scapy.**
```python
>>>p=scapy.sr1(scapy.IP(dst="192.168.1.1")/scapy.ICMP()/"test")
Begin emission:
Finished to send 1 packets.
*
Received 4 packets, got 1 answers, remaining 0 packets

>>>p
<IP  version=4 ihl=5 tos=0x0 len=32 id=6083 flags= frag=0 ttl=64 proto=icmp chksum=0xdfbf src=192.168.1.1 dst=192.168.1.9 options=[] |<ICMP  type=echo-reply code=0 chksum=0x1826 id=0x0 seq=0x0 |<Raw  load='test' |>>>

>>>p.show()
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