# Scapyѧϰ�ʼ�

python scapy DDoS

---
# Scapy��װ˵��

# Scapyʹ��˵��
> �ο��ĵ���http://blog.csdn.net/Al_xin/article/details/52305549

�������У�����Python����Python������
����import scapy.all as scapy 

```python
>>>import scapy.all as scapy
WARNING: No route found for IPv6 destination :: (no default route?). This affects only IPv6
```

�������������Ϣ����˵������������
```python
>>>scapy.IP()
<IP  |>
```

**ע��linux�����з�ʽ��windows��һ�������ϴ󲿷���������linux����˵���ġ�**

> �����ĵ���http://scapy.readthedocs.io/en/latest/#starting-scapy

���ͱ���

scapy.send(scapy.IP(dst="192.168.115.188")/scapy.ICMP())

**ע��windows��������Ҫ��ǰ׺scapy.**
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