# 学习Nginx的笔记
## Nginx基础
###  Nginx是什么
Nginx是高性能的HTTP和反向代理的服务器，处理高并发能力是十分强大的，能经受高负载的考验,有报告表明能支持高达 50,000个并发连接数。
### 反向代理
- 正向代理
    - 在客户端（浏览器）配置代理服务器，通过代理服务器进行互联网访问
      ![正向代理](.\images\forwardAgent.png)
    - 图解：用户想要访问google，但是无法直接访问，如果想要访问，需要代理服务器进行访问。因此需要在客户端配置代理服务器。这就是正向代理。
- 反向代理
    - 只需要将请求发送到反向服务器，由反向服务器去选择目标服务器获取数据后，再返回给客户端。此时反向代理服务器和目标服务器对外就是一个服务器，暴露的是代理服务器地址，隐藏了真实服务器IP地址。
    ![反向代理](.\images\forwardAgent.png)
- 区别
    - 正向代理是由用户配置代理服务器，然后通过代理服务器进行访问目标服务器。
    - 反向代理是用于访问代理服务器，然后由代理服务器选择最终的访问目标并返回资源。
### 负载均衡
- 当某一时间段请求并发量过多时，单个服务器解可能会回应缓慢，甚至直接崩溃。此时可以增加服务器的数量，然后将请求分发到各个服务器上。这种`将原先请求集中到单个服务器上的情况改为将请求分发到多个服务器上，将负载分发到不同的服务器`就是负载均衡。
![负载均衡](.\images\loadBalancing.png)

### 动静分离
- 为了加快网站的解析速度，可以把动态页面和静态页面由不同的服务器来解析，加快解析速度。降低原来单个服务器的压力。
![动静分离](.\images\resourceSeparate.png)


## nginx安装、常用命令和配置文件
Nginx可以安装在windows的环境中，但是在linux系统中效率更。所以一般安装在linux系统中。
### 在linux系统中安装nginx
1. 安装VMware虚拟机
2. 新建ubuntu系统
3. 安装nginx依赖
    - gcc：Nginx是c余元开发，安装nginx需要先将官网下载的源码进行编译，编译依赖gcc环境。
        - `sudo apt-get install build-essential`
        - `sudo apt-get install libtool`
        -  `yum install gcc-c++`
    - pcre:是一个Perl库，包括perl兼容的正则表达式库。nginx的http模块使用pcre来解析正则表达式，所以需要在linux上安装pcre库。
        - `sudo apt-get install libpcre3 libpcre3-dev`
        - `yum install -y pcre pcre-devel`
    - zlib: 提高了很多压缩和解压缩的方式，nginx使用zlib对http的内容进行gzip，所以需要在linux上安装zlib库
        - `sudo apt-get install zlib1g-dev`
        - `yum install -y zlib zlib-devel`
    - openssl：OpenSSL 是一个强大的安全套接字层密码库，囊括主要的密码算法、常用的密钥和证书封装管理功能及SSL协议，并提供丰富的应用程序供测试或其它目的使用。nginx不仅支持http协议，还支持https（即在ssl协议上传输http），所以需要在linux安装openssl库。
        - `sudo apt-get install openssl`
        - `yum install -y openssl openssl-devel`

### nginx常用命令
1. 进入 nginx 目录中：
`cd /usr/local/nginx/sbin`
2. 查看nginx版本号：`./nginx -v`
3. 启动 nginx ：`./nginx`
4. 停止 nginx ：`./nginx -s stop`
5. 重新加载 nginx ：`./nginx -s reload`
### nginx配置文件
1. nginx 配置文件位置<br> 
`cd /usr/local/nginx/conf/nginx.conf`
2. 配置文件中的内容<br>
    包含三部分内容
    1. `全局块`：配置服务器整体运行的配置指令。比如
        - worker_processes 1;处理并发数的配置 
    2. `events块`：影响 Nginx 服务器与用户的网络连接。比如
        - worker_connections 1024; 支持的最大连接数为 1024 
    3. `http块`：还包含两部分：`http全局`块以及`server块` 
## Nginx配置实例
### nginx配置实例1-反向代理
### nginx配置实例2-负载均衡
### nginx配置实例3-动静分离

## nginx配置高可用集群

## nginx原理
