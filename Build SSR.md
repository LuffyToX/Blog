# Build SSR



VPS 和 VPN 是两个经常容易混淆的术语，但是它们指的是两种完全不同的服务类型



VPS（Virtual Private Server，虚拟专用服务器）：托管公司提供的一种网站托管形式，为用户提供一个虚拟服务器环境来托管网站

网站托管有多种不同形式：独立主机、共享主机、VPS 主机、云主机等

VPS 主机使用虚拟化技术将单个物理服务器拆分成多个不同的虚拟服务器，每一个虚拟服务器都是一个私有服务器环境（不共享资源）

VPS 一般分为两种：Unmanaged、Managed

- Unmanaged VPS：相当于一台裸机，只提供一个原生操作系统，所有的软件都需要自己安装
- Managed VPS：已经安装好了各种建站软件，只需在后台点几个按钮就可以建好一个网站



VPN（Virtual Private Network，虚拟专用网络）： 一种允许用户在使用网络时保持完全私有性和匿名性的技术

VPN 通过公网与远程局域网建立一个临时的、安全的连接，为用户提供了一种保持匿名在线的方法，同时保护通过该连接传递的任何数据

开启 VPN 后，用户发送的任何请求都将被客户端加密后由公网传输到 VPN 服务器，然后 VPN 服务器再连接到互联网

***





### SS 与 SSR



SS（Shadowsocks）：一种 VPN 软件

SSR（Shadowsocks-R）：SSR 改进了混淆和协议，更难被防火墙检测到



SS/SSR 与 VPN 的区别

+ SS/SSR 基于 socks5 代理，客户端和实际要访问的服务端之间通过代理服务器进行通信，目的是转发客户端流量，绕过防火墙监测

+ VPN 是为了保证通信的安全性、私密性

***





### 创建谷歌云 VPS



<img src='https://img-blog.csdnimg.cn/20210603233423966.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjY0Nzc3,size_16,color_FFFFFF,t_70#pic_center' align='Left' style='width: 750px; height: 600px'/>



<img src='https://img-blog.csdnimg.cn/20210603233855751.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjY0Nzc3,size_16,color_FFFFFF,t_70#pic_center' align='Left' style='width: 800px; height: 400px'/>



<img src='https://img-blog.csdnimg.cn/20210604000605237.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjY0Nzc3,size_16,color_FFFFFF,t_70#pic_center' align='Left' style='width: 800px; height: 650px'/>



此时，只是创建了 VPS 实例，还需要配置防火墙（否则，SSR 不通）

<img src='https://img-blog.csdnimg.cn/20210604001750563.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjY0Nzc3,size_16,color_FFFFFF,t_70#pic_center' align='Left' style='width: 800px; height: 600px'/>



<img src='https://img-blog.csdnimg.cn/20210604002312913.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjY0Nzc3,size_16,color_FFFFFF,t_70#pic_center' align='Left' style='width: 800px; height: 500px'/>



<img src='https://img-blog.csdnimg.cn/2021060400334479.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjY0Nzc3,size_16,color_FFFFFF,t_70#pic_center' align='Left' style='width: 700px; height: 600px'/>



<img src='https://img-blog.csdnimg.cn/20210604003500592.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjY0Nzc3,size_16,color_FFFFFF,t_70#pic_center' align='Left' style='width: 760px; height: 650px'/>

***





### 远程登陆 VPS（此处以谷歌云 VPS 为例）



一、 本机生成 ssh 密钥对

```bash
# 首先查看本机是否已经存在 ssh 密钥对（window 默认路径：C:/Users/xxx/.ssh）
ls

# 如果已经存在，跳过此步；否则，执行如下命令（xxx 表示 user or email，用于登录 VPS）
ssh-keygen -t rsa -C 'xxx'

# 查看 .ssh 目录（私钥：id_rsa，公钥：id_rsa.pub）
cd ./.ssh

# 查看公钥
cat ./.ssh/id_rsa.pub
```



二、将 ssh 公钥（id_rsa.pub）复制到谷歌云 VPS

<img src='https://img-blog.csdnimg.cn/20210603212738955.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjY0Nzc3,size_16,color_FFFFFF,t_70#pic_center' align='Left' style='width: 750px; height: 590px'/>



<img src='https://img-blog.csdnimg.cn/20210603212950643.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjY0Nzc3,size_16,color_FFFFFF,t_70#pic_center' align='Left' style='width: 900px; height: 390px'/>



三、远程登陆 VPS

```bash
# user：ssh-keygen 中 'xxx' 的内容；ip：谷歌云 VPS 的外部 ip 
ssh user@ip
```

***





### VPS 安装 SSR 服务端



一、切换到 root

```bash
# sudo su / sudo su root / sudo -i
sudo su root
```



二、下载并运行一键安装脚本

```bash
bash <(curl -s -L https://git.io/v2ray.sh)
```

***





### SSR 加密、协议、混淆的选择



加密：使用 aes-256-gcm

协议：chain_a（chain_b虽说更难以被识别，但仍是一个测试版协议，并且实际使用发现丢包现象莫名十分严重，并不可用）

混淆：plain（不使用混淆，一切因使用混淆而产生的看似是网络加速了的效果都是因为绕过了限制，混淆实际上会减慢网络速度）

***





### 本机安装 SSR 客户端



<img src='https://img-blog.csdnimg.cn/20210603214108774.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjY0Nzc3,size_16,color_FFFFFF,t_70#pic_center' align='Left' style='width: 500px; height: 550px'/>

***





### 检查 IP 是否被墙



防火长城（GFW）：也称中国国家防火墙，是对中华人民共和国政府在其互联网边界审查系统的统称，专门针对一些国外网站进行封锁

如果 GFW 检测到代理服务器就会封锁代理服务器所用的 IP，被封锁后就无法使用了，也就是常说的被墙了



因为墙的是流量，因此进行可以检测，检测网址：https://www.vps234.com/ipchecker/

+ 国内 ICMP、TCP 不通  ==>  被墙  ==>  更换 IP
+ 国内和国外都不通  ==>  网络崩溃  ==>  重装（VPS）系统
+ 如果发现 IP 全通，但是网络没有通，基本就是端口被封

