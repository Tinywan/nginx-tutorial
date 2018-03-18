#### 1. 使用命令行安装

如果是在ubuntu系统下，可以直接使用命令行一键安装，安装完后也会自动启动nginx服务。

``` bash
$ sudo apt-get install nginx
```

如果是在mac下，可以使用brew安装。

``` bash
$ brew install nginx
```

#### 2. 源码编译安装

在生产环境下，我们可能需要下载源码编译安装，因为用命令行安装的方式，第一，自定义性不强，第二，可能安装包比较老。

登录到主机环境，这里以ubuntu系统安装目前的nginx稳定版本1.8.0为例。

在编译nginx之前先安装一些依赖的包。

``` bash
$ sudo apt-get install build-essential libc6 libpcre3 libpcre3-dev libpcrecpp0 libssl0.9.8 libssl-dev zlib1g zlib1g-dev lsb-base openssl libssl-dev  libgeoip1 libgeoip-dev  google-perftools libgoogle-perftools-dev libperl-dev  libgd2-xpm-dev libatomic-ops-dev libxml2-dev libxslt1-dev python-dev
```

接下来到官方网站下载nginx的源码包。

``` bash
# 下载源码包
$ wget http://nginx.org/download/nginx-1.8.0.tar.gz

# 解压
$ tar xvf nginx-1.8.0.tar.gz

# 进入目录并生成Makefile文件
$ cd nginx-1.8.0
$ ./configure \
--prefix=/etc/nginx                   \
--sbin-path=/usr/sbin/nginx           \
--conf-path=/etc/nginx/nginx.conf     \
--pid-path=/var/run/nginx.pid         \
--lock-path=/var/run/nginx.lock       \
--error-log-path=/var/log/nginx/error.log \
--http-log-path=/var/log/nginx/access.log \
--with-http_gzip_static_module        \
--with-http_stub_status_module        \
--with-http_ssl_module                \
--with-pcre                           \
--with-file-aio                       \
--with-http_realip_module             \
--without-http_scgi_module            \
--without-http_uwsgi_module           \
--without-http_fastcgi_module         \
```

上面的./configure命令我是按照自己的需要来定制安装，如果要简单点的话，直接运行`./configure`就好了。

关于上面的参数可以使用`nginx -V`来查看。

接下来编译并安装。

``` bash
$ make
$ sudo make install
```

这样就算安装成功。

要启动nginx，可以这样:

``` bash
$ sudo nginx
```

如果要停止服务，可以这样：

``` bash
$ sudo nginx -s quit
```

如果修改了配置文件，要重新生效，可以这样：

``` bash
$ sudo nginx -s reload
```

完结。
