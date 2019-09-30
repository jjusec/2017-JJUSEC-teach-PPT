
# 谈谈IP地址

BY ZZH JJUSEC

## 关于IP地址

ZZH有一台手机，ZZH还有一台电脑，办公室里有一个WIFI路由器，它发射的无线WIFI信号名字叫Doggen。

当手机连接上Doggen信号，电脑也连接上Doggen信号，那么WIFI路由器将会分别给电脑与手机一个IP地址，常以XXX.XXX.XXX.XXX形式表现。
如**192.168.0.100**和**192.168.0.101**。

那么路由器自己有IP地址吗，**当然有**，路由器的地址一般是**192.168.0.1**，路由器是连接了手机和电脑，此时路由器，手机，电脑便是一个小型**局域网**。

![](https://raw.githubusercontent.com/jjusec/issuer/master/network.png)


让我们再来看看手机的IP地址192.168.0.100和电脑的192.168.0.102和路由器的192.168.0.1。

我们发现**192.168.0**是他们共有的。

后面的192.168.0.**x**，
X会变动的，我们把前面相同的192.168.0称之为**网络号**，**x**是主机号，网络号相同表示手机与电脑在同一个局域网内。

在一个局域网内的设备都可以通过TCP/IP协议相互交流聊骚。除非一台机器有些自闭顺带开启了防火墙。

## 关于IP的几个误解

- 每台联网设备都有唯一的地址吗？<br><br>
是，也不是<br>IP地址由32位二进制数组成，为便于使用，常以XXX.XXX.XXX.XXX形式表现，每组XXX代表小于或等于255的10进制数，也就是说,192.168.1.999是不存在的。
整个的网络只能容纳4,294,967,296台机器，但是这个连咖啡机都能联网的魔法时代，给每台联网的设备一个独立唯一的ip地址是不存在的，除非你充钱。<br>

> IPv4的42億個地址的分配最終於2011年2月3日用盡

因为愚蠢的人类在设计IP协议的时候没想到魔法时代的来临，所以设计出了**局域网**这个概念。<br>
把一个价值连城的IP公网1.1.1.2给一个商人，这个商人在1.1.1.2下面组建网络号为100.100.x.X和101.101.x.x的小型局域网，
而局域网下面又分局域网，上网费用越来越贵，越来越慢。，这个商人便是X运营商。<br>

另外，一群聪明人提出了IPV6这个概念
> IPv6的优势就在于它大大地扩展了地址的可用空间，IPv6地址有128位长。如果地球表面（含陆地和水面）都覆盖着计算机，
那么IPv6允许每平方米拥有7*10^23个IP地址；如果地址分配的速率是每微秒100万个，那么需要10^19年才能将所有的地址分配完毕。

是不是很流弊，近期（10年）应该就能普及，看来网络工程的学生头发不保。

回到正题，在同一个局域网内，我们的IP是唯一的，但不代表在别的局域网内，我们的IP还是唯一的。

- 知道了IP就可以黑掉ta电脑？<br>
我就这表情<br>
![YYF](https://ws1.sinaimg.cn/large/006tKfTcgy1fpvciww77xj30gm09c450.jpg)





## 再谈谈ping命令

即使我们在同一个局域网下，也有可能存在你我不联通的情况，如A在WIFI路由器的边上，B在与WIFI路由器隔着几道水泥墙，那么B的接受到的信号会非常的弱，
A与B可能出现无法我法联通的情况。但光靠猜想是不行的，我们可以用ping命令去检测A与B的联通情况。

A的ip地址是`192.168.42.100`

B的ip地址是`192.168.42.129`

A想要知道B是否与自己联通，可以在命令行终端下执行`ping 192.168.42.129`

A 通过ping 呼叫B，B会立即做应答。


```bash
PING 192.168.42.129 (192.168.42.129) 56(84) bytes of data.
64 bytes from 192.168.42.129: icmp_seq=1 ttl=64 time=3.53 ms
64 bytes from 192.168.42.129: icmp_seq=2 ttl=64 time=2.37 ms
64 bytes from 192.168.42.129: icmp_seq=3 ttl=64 time=2.88 ms
64 bytes from 192.168.42.129: icmp_seq=4 ttl=64 time=2.53 ms
^C
--- 192.168.42.129 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3004ms
rtt min/avg/max/mdev = 2.366/2.825/3.526/0.445 ms
```

`0% packet loss`表示发送的数据包丢失了0%，说明联通性很好。

这里给ping来个比较准确的定义:
> ping 程序是用来探测主机到主机之间是否可通信，如果不能ping到某台主机，表明不能和这台主机建立连接。ping 使用的是ICMP协议，
它发送icmp回送请求消息给目的主机。ICMP协议规定：目的主机必须返回ICMP回送应答消息给源主机。如果源主机在一定时间内收到应答，则认为主机可达。




我们还可以用ping来测试我们是否连接上了广域互联网，如，我们时候可以上baidu.com，是否可以上google.com，或者测试一台主机是否存活，或者是否开启了防火墙。

打开命令行终端，执行ping命令看看吧～

例子：`ping baidu.com`

```bash
zzh@Gentoo ~ % ping  baidu.com
PING baidu.com (220.181.38.148) 56(84) bytes of data.
64 bytes from 220.181.38.148 (220.181.38.148): icmp_seq=1 ttl=48 time=48.5 ms
64 bytes from 220.181.38.148 (220.181.38.148): icmp_seq=2 ttl=48 time=66.0 ms
64 bytes from 220.181.38.148 (220.181.38.148): icmp_seq=3 ttl=48 time=136 ms
64 bytes from 220.181.38.148 (220.181.38.148): icmp_seq=4 ttl=48 time=132 ms
^C
--- baidu.com ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3004ms
rtt min/avg/max/mdev = 48.512/95.521/135.714/38.770 ms
```


例子： `ping google.com`

```bash
zzh@Gentoo ~ % ping google.com
PING google.com (216.58.200.23) 56(84) bytes of data.
^C
--- google.com ping statistics ---
3 packets transmitted, 0 received, 100% packet loss, time 2032ms

```

看来`google`是一个并不存在网站：）

下一节将讨论GET/POST请求

