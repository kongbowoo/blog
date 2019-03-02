* 将unbuntu支持桌面系统

```shell
apt-get update
apt-get install ubuntu-desktop
```

* 安装后需要重启系统


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
