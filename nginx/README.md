


# Mac 上

## 安装

brew install nginx

检查nignx是否安装成功

nginx -V 查看nginx版本及安装的本地位置

ngxin -v 查看nginx版本（此方法依然可以检测是否安装某一软件，如git,hg等）

//同时你也可以在浏览器上输入,来查看运行结果,出现下图应该就可以了
localhost:80

## 启动

如果没有启动，需要手动启动

sudo nginx -c /usr/local/etc/nginx/nginx.conf


## 停止

在终端中输入 ps -ef|grep nginx 获取到nginx的进程号，注意是找到“nginx:master”的那个进程号，如下面的进程好是 15800

501 15800 1 0 12:17上午 ?? 0:00.00 nginx: master process /usr/local/Cellar/nginx/1.8.0/bin/nginx -c /usr/local/etc/nginx/nginx.conf

501 15801 15800 0 12:17上午 ?? 0:00.00 nginx: worker process

501 15848 15716 0 12:21上午 ttys000 0:00.00 grep nginx

在终端中输入以下几种命令都可以停止

kill -QUIT 15800 (从容的停止，即不会立刻停止)

Kill -TERM 15800 （立刻停止）

Kill -INT 15800 （和上面一样，也是立刻停止）

## 重启

如果只是修改了配置，没有必要重启，只需要重新加载配置
```
nginx -s reload
```

快速停止或关闭Nginx：nginx -s stop
正常停止或关闭Nginx：nginx -s quit



## 配置

```
  -v            : show version and exit // 告诉我们nginx的配置信息
  -V            : show version and configure options then exit // 不仅告诉我们配置信息，还会告诉我们配置选项，然后停止
  -t            : test configuration and exit // 检查配置是不是正确 如果配置文件不正确的话，可以使用 nginx -c location 来指定配置文件
  -T            : test configuration, dump it and exit // 检查配置，并把这些配置打印出来，然后就停止
  -q            : suppress non-error messages during configuration testing 
  -s signal     : send signal to a master process: stop, quit, reopen, reload // 给主进程发信息，比如stop, quit, reopen, reload这些指令（Quit 是一个优雅的关闭方式，Nginx在退出前完成已经接受的连接请求；Stop 是快速关闭，不管有没有正在处理的请求）
  -p prefix     : set prefix path (default: /usr/local/Cellar/nginx/1.15.5/) // -s reopen 重新打开日志（不懂日志）
  -c filename   : set configuration file (default: /usr/local/etc/nginx/nginx.conf) // nginx到底以哪个配置文件为准
  -g directives : set global directives out of configuration file
```

这个时候我们可以先执行 `nginx -V` 然后会看到 nginx 的配置信息

```
nginx version: nginx/1.13.10
built by clang 9.0.0 (clang-900.0.39.2)
built with OpenSSL 1.0.2n  7 Dec 2017 (running with OpenSSL 1.0.2q  20 Nov 2018)
TLS SNI support enabled
configure arguments: --prefix=/usr/local/Cellar/nginx/1.13.10 --sbin-path=/usr/local/Cellar/nginx/1.13.10/bin/nginx --with-cc-opt='-I/usr/local/opt/pcre/include -I/usr/local/opt/openssl/include' --with-ld-opt='-L/usr/local/opt/pcre/lib -L/usr/local/opt/openssl/lib' --conf-path=/usr/local/etc/nginx/nginx.conf --pid-path=/usr/local/var/run/nginx.pid --lock-path=/usr/local/var/run/nginx.lock --http-client-body-temp-path=/usr/local/var/run/nginx/client_body_temp --http-proxy-temp-path=/usr/local/var/run/nginx/proxy_temp --http-fastcgi-temp-path=/usr/local/var/run/nginx/fastcgi_temp --http-uwsgi-temp-path=/usr/local/var/run/nginx/uwsgi_temp --http-scgi-temp-path=/usr/local/var/run/nginx/scgi_temp --http-log-path=/usr/local/var/log/nginx/access.log --error-log-path=/usr/local/var/log/nginx/error.log --with-debug --with-http_addition_module --with-http_auth_request_module --with-http_dav_module --with-http_degradation_module --with-http_flv_module --with-http_gunzip_module --with-http_gzip_static_module --with-http_mp4_module --with-http_random_index_module --with-http_realip_module --with-http_secure_link_module --with-http_slice_module --with-http_ssl_module --with-http_stub_status_module --with-http_sub_module --with-http_v2_module --with-ipv6 --with-mail --with-mail_ssl_module --with-pcre --with-pcre-jit --with-stream --with-stream_realip_module --with-stream_ssl_module --with-stream_ssl_preread_module
```

- --conf-path 指定了 nginx 的配置文件的位置

打开 `--conf-path` 指定的配置文件。先看看nginx主要的配置，及它们的含义

```
worker_processes  4;  #Nginx运行时使用的CPU核数

events {
    worker_connections  1024;  #一个woeker进程的最大连接数
}

http {  #Nginx用作虚拟主机时使用。每一个server模块生成一个虚拟主机。

    include       mime.types;  #定义MIME类型和后缀名关联的文件的位置
    default_type  application/octet-stream;  #指定mime.types文件中没有记述到的后缀名的处理方法

    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '  #定义日志的格式。可以选择main或者ltsv，后面定义要输出的内容。
　　　　　　　　　　　　　'$status $body_bytes_sent "$http_referer" '
 
　　　　　　　　　　　　　'"$http_user_agent" "$http_x_forwarded_for"'; 

    
 1.$remote_addr 与$http_x_forwarded_for 用以记录客户端的ip地址；
 2.$remote_user ：用来记录客户端用户名称；
 3.$time_local ：用来记录访问时间与时区；
 4.$request ：用来记录请求的url与http协议；
 5.$status ：用来记录请求状态； 
 6.$body_bytes_s ent ：记录发送给客户端文件主体内容大小；
 7.$http_referer ：用来记录从那个页面链接访问过来的；
 8.$http_user_agent ：记录客户端浏览器的相关信息；。


    access_log  /usr/local/var/log/nginx/access.log  main;  #连接日志的路径，上面指定的日志格式放在最后

    sendfile        on;  #是否使用OS的sendfile函数来传输文件
    keepalive_timeout  65;  #HTTP连接的持续时间。设的太长会使无用的线程变的太多


    server { 
        listen       80;  #监听端口
        server_name  localhost;  #服务地址

        charset utf-8;   #编码方式

        access_log  /usr/local/var/log/nginx/localhost.access.log  main;  #nginx请求日志地址

        root /var/www; #你的网站根目录
        location / { # 所有的请求都会走的路径
            index  index.html index.htm index.php;
        　　 try_files $uri /$uri index.php?$args;  #从左边开始找指定文件是否存在
        }
     

        error_page  404              /404.html;
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }

        location ~ \.php$ {  # 正则表达式: .php文件走的路径
            fastcgi_pass   127.0.0.1:9000; #走fastcgi 路径
            fastcgi_index  index.php;
            fastcgi_param  SCRIPT_FILENAME  /var/www$fastcgi_script_name; #定义的根目录 以及 请求的脚本名
            include        fastcgi_params; # 请求参数
        }
   
        location ~ /\.ht { # 当前项目的根路径
            deny  all;
        }
    }

    include sites-enabled/nginx-*.conf;   # 添加的文件其他虚拟主机配置
}
```

### 修改 nginx 的配置文件

有一行
```
include servers/*;
```
这是 `server { ... }`  部分的配置，将它修改为

```
include servers/*.conf
```

如果有 `include valet/valet.conf` 和 `include "/Users/yaowen/.config/valet/Nginx/*"` 可以将其注释或者删除， valet 是轻量级的 laraval 框架。 Magento 不需要。


这样就能只导入以 `.conf` 结尾的配置文件。以防这个目录放置了其他文件也被导入，但这也限制了配置文件必须以 `.conf` 结尾

将 docker 镜像配置文件 `images/nginx/conf.d/default_ip.conf` 拷贝到 `/usr/local/etc/nginx/servers` 目录下。 同时将内容修改为

```
server {
    listen 80;
    server_name _;

    set $MAGE_ROOT /Users/yaowen/php/web_magento_shopping_site; # 自己电脑的项目根目录
    set $MAGE_DEBUG_SHOW_ARGS 1;

    include servers/CommonMagento.main; # 要拷给的另一个文件
}
```

如上的文件中， `CommonMagento.main` 也需要拷贝， 将docker 镜像配置文件 `images/nginx/conf.d/CommonMagento.main` 和 `images/nginx/conf.d/CommonPhpUpstream.conf`也拷贝到 `/usr/local/etc/nginx/servers` 目录下。

修改拷贝来的 `CommonPhpUpstream.conf`， 由于 docker 中的 php 配置了负载均衡，有多个 php docker，本地仅适用一个即可。文件内容为

```
# php upstream
upstream fastcgi_backend {
    server 127.0.0.1:9000;
}
```

如上，由于 php 适用的是端口代理，需要确定本地的 php-fpm 也是使用的 `9000` 端口访问的方式。 所以需要确认一下 php-fpm 的配置。 

MAC 自带了 php-fpm，查找 `php-fpm.conf` 的位置

```
php-fpm -t // 检测配置
```

打开显示的配置文件。用;注释掉sock监听的方式，增加9000端口监听。

```
[www]
#listen = /tmp/php-cgi-56.sock
listen = 9000
```

如果该文件不存在这个配置，可以查看 `include` 导入的配置，例如，我的在最后一行有 `include=/usr/local/etc/php/7.1/php-fpm.d/*.conf`， 去这个目录找所有的 `.conf` 文件， 如果没有以 `.conf` 结尾的文件，应该是使用的 MAC 自带的 php-fpm 的配置文件 `/private/etc/php-fpm.conf`，其结构跟 php 的结构完全一样。修改之后同样要重启 php-fpm 才能生效

```
sudo php-fpm
```

如果出先错误

```
502 Bad Gateway nginx/xxx
```
请检查 php-fpm 的sock监听 `listen = 9000` 配置是否修改生效了。


## PHP

php --ini 查看 php.ini 位置


有时候 Magento 的一些依赖扩展不足，例如 'pcntl'， 其实是环境没有配置好，查看 PATH 路径是否具有 `/usr/local/opt/php@7.1/bin`， 如果没有，添加如下内容。 这里是针对 bash 是 zsh 的，对于 bash 可以网上搜多添加到 `PATH` 环境变量即可。 

配置 PHP 路径

echo 'export PATH="/usr/local/opt/php@7.1/bin:$PATH"' >> ~/.zshrc
echo 'export PATH="/usr/local/opt/php@7.1/sbin:$PATH"' >> ~/.zshrc

配置完后， php 环境可能没有生效，记得重启 php-fpm 或者重启电脑。我记得我重启 php-fpm 也没有生效，不知道是不是没重启成功，最后重启的电脑。

出现错误

```
In Brew.php line 204:

  Homebrew PHP appears not to be linked.
```

运行指令

```
brew link php@7.1 --force --overwrite
```
### Installing extensions

Extensions such as php-xdebug and php-mongodb have been removed and now should be installed from PECL:

```
pecl install xdebug 
```

## 查看端口占用

```
lsof -i :9000
```


## 重启 php 服务

启动 php 服务
```
sudo php-fpm
或者
brew services restart php@7.1
```


```
ERROR: failed to open configuration file '/private/etc/php-fpm.conf': No such file or directory (2
```

错误信息显示，不能打开配置文件，cd /private/etc，发现没有 php-fpm.conf 文件，但是有 php-fpm.conf.default 文件。这个文件是默认配置，我们可以复制一份，改名为 php-fpm.conf，然后再根据需要改动配置。

cp /private/etc/php-fpm.conf.default /private/etc/php-fpm.conf



错误
```
ERROR: failed to open error_log (/usr/var/log/php-fpm.log): No such file or directory (2)
```
由于 `/private/etc` 普通用户没有写权限。修改配置

```
sudo vim /private/etc/php-fpm.conf
```

修改 error_log 为

```
error_log = /usr/local/var/log/php-fpm.log
```

执行 php-fpm -t，这个世界终于清净了！




## 安装 magento 依赖

访问浏览器 localhost:8080 时 出现

```
Autoload error
Vendor autoload is not found. Please run 'composer install' under application root directory.
```

说明能够正常访问项目了，这时候需要进入项目目录下，安装 php 依赖

```
cd 项目目录
composer install
```
期间会让输入用户名和密码才能继续下载

```
用户名: 13656669040d7a75bb0b3f04d4b06ea5
密码: d159f01b2a35a875a34b69c9e6dca33f
```

拷贝别人的 `app/etc/env.php` 到自己项目目录对应的目录中。该文件是数据库、缓存等的配置文件。



如果发现没有样式，在项目根目录先执行

```
php bin/magento setup:upgrade
php -dmemory_limit=3G bin/magento setup:di:compile
php -dmemory_limit=3G bin/magento setup:static-content:deploy en_US -f
php -dmemory_limit=3G bin/magento indexer:reindex
php bin/magento cache:clean && php bin/magento cache:flush
```

在执行第二个指令的时候，有可能出现内不能不够的情况，修改 `/usr/local/etc/php/7.1/php.ini`

```
# memory_limit = 128M
memory_limit = 2048M
```
然后使用命令 `php -dmemory_limit=3G bin/magento setup:di:compile` 代替第二个命令。

在项目根目录下执行如下指令，添加访问权限

```
ind var generated vendor pub/static pub/media app/etc -type f -exec chmod g+w {} +
find var generated vendor pub/static pub/media app/etc -type d -exec chmod g+ws {} +
chown -R :www-data .
chmod u+x bin/magento
```
给 `var` 和 `var/cache` 添加访权限。

```
chmod o+w var
chmod o+w var/cache
```

 
加载网页比较慢，开启所有缓存。在项目根目录下执行

```
php bin/magento cache:enable
```

修改 env.php 配置后，清除一下缓存才会生效。 在项目根目录下执行

```
bin/magento cache:flush 
```


## 常用指令

> 重启 php-fpm

查看php-fpm端口是否在被php-fpm使用
```
sudo lsof -i:9000
```

一般修改 php.ini 文件后经常需要重启php-fpm
```
sudo  killall  php-fpm   // 关闭
```

再输入 sudo lsof -i:9000 就会发现php-fpm没有打印对应端口
```
sudo  php-fpm    // 重启
```








<div class="product-three-block-title-container">
<div class="product-three-block-title-line" style="overflow: hidden; zoom: 1;">&nbsp;</div>
<h2 class="product-three-block-title">Featured collection</h2>
</div>
<div class="row product-three-block">
<div class="product-item" style="background-image: url('{{media url=&quot;wysiwyg/5.jpg&quot;}}"><a href="index.html"> <img class="product-image" src="{{media url=&quot;wysiwyg/5.jpg&quot;}}" width="400" height="400"></a>
<div class="bottom-container">
<div class="product-title">Title</div>
<div class="product-desc">Description</div>
<div><span class="product-price">$ 232</span> <span class="product-detail-entry">Buy now &gt;</span></div>
</div>
</div>
<div class="product-item" style="background-image: url('{{media url=&quot;wysiwyg/5.jpg&quot;}}"><a href="index.html"> <img class="product-image" src="{{media url=&quot;wysiwyg/6.jpg&quot;}}" width="1000" height="1000"></a>
<div class="bottom-container">
<div class="product-title">Title</div>
<div class="product-desc">Description</div>
<div><span class="product-price">$ 232</span> <span class="product-detail-entry">Buy now &gt;</span></div>
</div>
</div>
<div class="product-item" style="background-image: url('{{media url=&quot;wysiwyg/5.jpg&quot;}}"><a href="index.html"> <img class="product-image" src="{{media url=&quot;wysiwyg/8.jpg&quot;}}" width="1000" height="1000"></a>
<div class="bottom-container">
<div class="product-title">Title</div>
<div class="product-desc">Description</div>
<div><span class="product-price">$ 232</span> <span class="product-detail-entry">Buy now &gt;</span></div>
</div>
</div>
<div style="clear: both;">&nbsp;</div>
</div>




