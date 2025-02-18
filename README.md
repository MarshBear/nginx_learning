# nginx 学习笔记

[nginx](https://nginx.org/)是一款轻量级的 Web 服务器 、反向代理服务器。完整的 nginx 文档可见[nginx 官方文档](https://nginx.org/en/docs/)，本文档仅用于记录 nginx 学习过程，主要使用 nginx 的反向代理与负载均衡的功能。

### 反向代理

所谓反向代理即用户向服务器发送的请求先传入到 nginx 服务器，再由 nginx 服务器转发到内部网络上。“代理”一词往往用在客户端，在网络结构中用户上网需要通过网关将请求传出去，用户和外网不直接互通，需要网关作为代理服务器连接。“反向代理”一次由此而来，作用于服务端，用户发送的请求不能直接触达服务器内部网络，需要经过 nginx 代理才能达到。

<figure><img src="./images/reverse-proxy.png" alt=""><figcaption><p>正向代理与反向代理</p></figcaption></figure>

通常这种代理模式称为**隧道式代理**，即进出流量都走代理这一个通道。这样的代理方式使得网络瓶颈很容易出现在代理服务器上，若代理服务器的性能不足时，不论增加服务端还是客户端的带宽都无法增加性能，服务上限首代理服务器约束。除了 nginx 作反向代理，还有一些代理方式能一定程度解决这样的约束，如 LVS 采用的 DR 模式，访问服务器时经过反向代理，而返回数据时不经过代理直接触达客户端，减少代理服务器的流量压力。

### nginx 还能做什么

出了反向代理，nginx 在实际业务中有很多其他的作用。事实上 nginx 最简单的点就是做负载均衡，网站在运营中大部分是以集群方式运行，需要使用负载均衡来分流，nginx 也可以实现简单的负载均衡功能。除此之外还可以做简单的 URL 改写方便业务逻辑转发等等简单应用。
