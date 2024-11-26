# TPBox-ForAnddroid

<span style="color: #41b349; font-size: 15px; font-weight: bold;">软件说明:</span>

- 一款基于`sing-box`编写的`安卓通用代理客户端`
- sing-box 版本: `fork 1.10.2`
- sing-box项目地址: https://github.com/SagerNet/sing-box

- 原版在1.6.0版本中舍弃了`SSR`协议`fork版本`中再次添加了`SSR`协议
- `SSR代码`来自`mihomo`的meta分支
- mihomo项目地址: https://github.com/MetaCubeX/mihomo

<span style="color: #41b349; font-size: 13px; font-weight: bold;">运行模式:</span>

- 软件共有`3种`运行模式:
- `VPN`: 使用系统VPN代理
- `TUN`: 使用sing-box-tun(透明代理)
- `仅代理`: 启动一个本地代理
- `TUN模式`需要`root权限`才能使用
- `VPN`与`TUN`的区别: VPN`需要`软件常驻后台，而TUN模式则`不需要`

<span style="color: #41b349; font-size: 15px; font-weight: bold;">使用说明:</span>

- 没有出现在`该文档`其余协议与`原版`没有区别
- 官方文档地址: https://sing-box.sagernet.org/zh/

###### 路由设置

- `远程路由文件`仅支持后缀为`.srs`的`sing-box专用`路由文件
- 其他规则项`填写格式`全部都为`一行一条`
- `已添加`的路由项可以`长按拖动排序`
- 因为sing-box的路由规则`优先级是从上到下`的

###### 订阅设置

- 订阅仅支持`一行一条节点url`的内容格式
- Base64编码或者不编码都可以

###### 链式代理

- 对于已添加的节点可以`长按拖动排序`

###### HTTP协议

- 对于`HTTP协议`进行了一些`小的更改`
- `以下`是更改后`与原版的区别`

<span style="color: #41b349; font-size: 13px; font-weight: bold;">路径说明:</span>

- 假设填写`路径`为 `/path`

- 原版sing-box握手过程

```plaintext
CONNECT /path HTTP/1.1
Host: www.example.com:443
User-Agent: Go-http-client/1.1
Proxy-Connection: Keep-Alive
```

- 修改后握手过程

```plaintext
CONNECT www.example.com:443/path HTTP/1.1
Host: www.example.com:443
User-Agent: Go-http-client/1.1
Proxy-Connection: Keep-Alive
```

-至于有什么用呢?(懂的都懂)

```plaintext
路径填写: @gw.alicdn.com

CONNECT www.example.com:443@gw.alicdn.com HTTP/1.1
Host: www.example.com:443
User-Agent: Go-http-client/1.1
Proxy-Connection: Keep-Alive
```

<span style="color: #41b349; font-size: 13px; font-weight: bold;">请求头说明:</span>

- 自定义请求头跟原版没有区别

- 填写格式(一行一条)

```plaintext
Host: www.google.com
User-Agent: okhttp/4.12.0
```

- 握手过程

```plaintext
CONNECT www.example.com:443 HTTP/1.1
Host: www.google.com
User-Agent: okhttp/4.12.0
Proxy-Connection: Keep-Alive
```

<span style="color: #41b349; font-size: 13px; font-weight: bold;">Del Host 说明:</span>

- 开启`Del Host`后握手时会删除host字段

- 握手过程

```plaintext
CONNECT www.example.com:443 HTTP/1.1
User-Agent: Go-http-client/1.1
Proxy-Connection: Keep-Alive
```

- 至于有什么用呢?

- 某度直连的http代理在握手时需要添加一个`X-T5-Auth`头来作为身份验证,开启`Del Host`后你会发现`就算没有添加身份验证`
  也可以`握手成功`,其他作用自行探索。

- 如果添加的`自定义请求头`中包含`Host`,`Del Host`将无效

<span style="color: #41b349; font-size: 13px; font-weight: bold;">其他注意:</span>

- 设置中的`Github代理`是用于下载远程路由文件的,如果`代理失效`请`自行更换`别的代理

- 因为`软件设计`问题`不允许节点昵称重复`如果`导入的节点`与`已导入的节点`重名软件会`自动重命名`所以不必`大惊小怪`
