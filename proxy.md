# 什么是代理（proxy）

## 我们正常上baidu的时候情况是这样的：

**发送数据：**

ZZH ----------> baidu.com

**接受数据：**

ZZH <---------- baidu.com


## 有代理的时候（PROXY）：

**发送数据**

ZZH ----->（PROXY）----> baidu.com

**接受数据**

ZZH <-----（PROXY）<---- baidu.com

# 代理vs代理程序vs代理服务器
代理分很多种，如**HTTP/HTTPS/SOCKS**代理，

代理程序是一个计算机程序，它有魔法，能拦截处理和修改ZZH发送给baidu的数据包。用来加密数据绕过网络封锁的代理程序有Shadowsocks,Tor,某VPN。用来修改拦截数据
的代理程序有Zaproxy,burpsuit,privoxy。

当一个服务器运行一个代理程序的时候，我们把它叫做代理服务器。

# 代理服务器真的可以为所欲为


正常情况下，ZZH与他对象聊天；

ZZH发送消息[我喜欢你~] -----------------------------> 对象<br>
ZZH <-------------------------------------------- 对象返回消息[我也喜欢你~]<br>
     
     
当ZZH用了X流氓免费VPN代理的时候：

ZZH发送消息[我喜欢你]------------------>代理服务器篡改消息[ZZH喜欢男人]-------------------> 对象[???!!!!!]

![what?](https://raw.githubusercontent.com/jjusec/issuer/master/sticker1.webp)






