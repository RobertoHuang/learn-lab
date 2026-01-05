容器网络是指容器相互连接和通信，以及与非Docker服务连接和通信的能力

# bridge网络

默认情况下Docker提供三种网络

![image-20260104224052086](./images/image-20260104224052086.png)

如果创建容器时不指定任何参数，那么容器将绑定到默认的`bridge`网络中

通过命令`docker network inspect f83613334890`可以查看绑定到该网桥的信息

![image-20260104223800559](./images/image-20260104223800559.png)

如果两个容器绑定到一个网桥上，那他们就可以通信了



使用`docker create`或`docker run`创建或运行容器时，桥接网络上所有容器的端口都可以从Docker主机和连接到同一网络的其他容器访问。但是这些端口无法从主机外部访问，在默认配置下也无法从其他网络中的容器访问

使用端口映射`-p`使端口在主机外部可用，并可提供其他桥接网络中的容器，示例

```
docker container run -d  -p 80:80 nginx
```



# host网络

使用场景: 为了网络的性能优化



如果容器使用`host`网络模式，则该容器的网络不会和Docker宿主机隔离(共享主机的网络命名空间)

并且容器不会分配自己的IP地址

例如: 如果你运行一个绑定到80端口的容器，并且使用`host`网络模式，则容器将无法获取自己的IP地址

在网络连接方面，容器的应用程序可通过主机IP地址的80端口范围。以Nginx为例

```
docker run --net=host -d nginx
```

使用`host`模式下的网络配置，容器在使用时没有自己的IP地址。所以端口映射将不起作用。如`-p` 、`-P`等端口映射参数将被忽略



# none网络

`none`网络是Docker提供的完全隔离模式，当你为一个容器分配一个`none`网络时，这个容器就像是一个没插网线的断网的主机

进入这种容器，通过`ip addr`命令只能看到一个本地回环接口`lo`，没有`eth0`没有IP地址，也没有任何外部路由。他适用于敏感数据处理等场景



# Docker网络互通原理推荐学习

在学习Docker网络过程中，也补充了一些网络相关的知识点

如果你是一个好奇宝宝的话，可以通过以下教程深入理解Docker的网络知识

- [这一次，让我在百度告诉你，当你请求www.baidu.com时都发生了什么？](https://mp.weixin.qq.com/s/YiC-WHmn-DQwUzGsN3TXrg)

- [放点存货：白日梦的Docker网络笔记](https://mp.weixin.qq.com/s/W8TIdjs3RrqFA92X79yyKw)
- [你还不懂Docker容器间网络互联原理吗？来白嫖啊...... 建议收藏哦](https://mp.weixin.qq.com/s/Pfp91R7bWz-QKhDD_JerPg)
- [白日梦的网络笔记：iptables、防火墙](https://mp.weixin.qq.com/s/bwK_ECwmL6OAjKHkiqGNpA)

- [用iptables搭建一套强大的安全防护盾](https://www.imooc.com/learn/389)

怎么验证自己看完这些文章之后，对Docker网络的了解程度呢？你可以尝试一下 是否能回答如下这些问题

- Docker容器间网络通信是怎么实现的？
- Docker容器是如何做到能访问外网的？
- 外部服务器对Docker容器的访问 实现原理？
- Docker网络不同的网桥之前是怎么做到网络隔离的？为什么需要两阶段？

