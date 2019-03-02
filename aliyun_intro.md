* 将unbuntu支持桌面系统
apt-get update
apt-get install ubuntu-desktop

reboot


```shell
root@iZ2zeiw4hobozk3k0gd9yaZ:~# cd /usr/share/lightdm/lightdm.conf.d/
root@iZ2zeiw4hobozk3k0gd9yaZ:/usr/share/lightdm/lightdm.conf.d# vim 50-ubuntu.conf
```
* 增加如下两行代码：
```shell
[Seat:*]
user-session=ubuntu
greeter-show-manual-login=true
allow-guest-false
```
