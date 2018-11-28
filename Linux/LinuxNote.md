#Linux Note 笔记

* 当远程访问 linux 服务时，发现访问失败时。 原因通常是 Linux 自带的 防火墙导致的。
 *防火墙种类： 1、firewalld      2、iptables 两种

```html
关闭防火墙命令：systemctl stop firewalld.service

开启防火墙：systemctl start firewalld.service

关闭开机自启动：systemctl disable firewalld.service

开启开机启动：systemctl enable firewalld.service

```
