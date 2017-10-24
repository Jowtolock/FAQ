#### 安装Nginx/Tengine防护模块
>云锁适配Nginx版本，是使用已经预编译好的包含云锁模块的Nginx替换掉您当前系统中使用的Nginx。但当您的Nginx含有以下参数时，需编译安装。
>
`--add-module


**建议：**在安装防护模块前先重启一次Nginx的服务，确保业务重启后可以正常运行，然后再安装云锁防护模块。

1. 编译前先将已经安装的Nginx文件进行备份，通过ps命令查看nginx文件的路径。以下所有步骤都以自身nginx路径为准。
       # ps -elf | grep nginx

 ![](/assets/Nginx filter_0.png)
       # cd /usr/local/nginx/sbin/
       # cp nginx nginx.bak

 ![](/assets/Nginx filter_1.png)
2. 有源码包则忽略此步骤。无源码包则到[Nginx官网](http://nginx.org/en/download.html)下载Nginx源码包，源码包需与自己的当前Nginx版本匹配（假设当前Nginx版本为1.10）
       # wget http://nginx.org/download/nginx-1.10.1.tar.gz

 ![](/assets/Nginx filter_2.png)
3. 解压nginx源码包
       # tar zxvf nginx-1.10.1.tar.gz

 ![](/assets/Nginx filter_3.png)
4. 由于其不支持post过滤，所以需要修改Nginx文件。1.8.0 版本以下需修改源码目录下`ngx_http_upstream.c`文件，1.8.0 以上还可以通过修改`configure`后的`Makefile`文件支持（详见第9步），**Tengine则跳过该步骤**。在`static void ngx_http_upstream_init_request(ngx_http_request_t \*r);`行上方添加：`int ngx_http_yunsuo_post_in_handler(ngx_http_request_t *r);`和在`ngx_http_upstream_init_request`后，添加：

       if (ngx_http_yunsuo_post_in_handler(r)) {
           return;
       }

       # cd nginx-1.10.1/src/http/
       # vim ngx_http_upstream.c
       --------------------下面这段是添加的----------------
       int
       ngx_http_yunsuo_post_in_handler(ngx_http_request_t *r);
       -----------------------------------------------
       static void
       ngx_http_upstream_init_request(ngx_http_request_t *r)
       {
       ngx_str_t                      *host;
       ngx_uint_t                      i;
       ngx_resolver_ctx_t             *ctx, temp;
       ngx_http_cleanup_t             *cln;
       ngx_http_upstream_t            *u;
       ngx_http_core_loc_conf_t       *clcf;
       ngx_http_upstream_srv_conf_t   *uscf, **uscfp;
       ngx_http_upstream_main_conf_t  *umcf;
       --------------------下面这段是添加的----------------
       if (ngx_http_yunsuo_post_in_handler(r)) {
           return;
       }
       ------------------------------------------------
       if (r->aio) {
           return;
       }

 ![](/assets/Nginx filter_4.png)
5. 下载云锁防护模块压缩包
       # cd /root/
       # wget https://codeload.github.com/yunsuo-open/nginx-plugin/zip/master -O nginx-plugin-master.zip

 ![](/assets/Nginx filter_5.png)
6. 解压云锁防护模块压缩包nginx-plugin-master.zip
       # unzip nginx-plugin-master.zip

 ![](/assets/Nginx filter_6.png)
7. 获取当前云锁模块所在目录的全路径
       # cd nginx-plugin-master/
       # pwd

 ![](/assets/Nginx filter_7.png)
8. 查看当前nginx加载的模块，在编译加载云锁防护模块的时候仍需加载这些模块
       # /usr/local/nginx/sbin/nginx –V

 ![](/assets/Nginx filter_8.png)
9. 进入nginx源码目录，对nginx进行编译；编译时添加云锁防护模块参数，参数路径为第7步获取的云锁防护模块源码全路径“/root/nginx-plugin-master”
       # cd nginx-1.10.1/
       # ./configure --prefix=/usr/local/nginx --with... --add-module=/root/nginx-plugin-master

 ![](/assets/Nginx filter_9.1.png) 

 1.8.0 以上要支持post过滤，在objs/Makefile文件中的CFLAGS后追加宏定义 HIGHERTHAN8
        # vim objs/Makefile
        CFLAGS =  -pipe  -O -W -Wall -Wpointer-arith -Wno-unused-parameter -Werror -g -DHIGHERTHAN8

 ![](/assets/Nginx filter_9.2.png)

 configure完成后进行make
        # make

 ![](/assets/Nginx filter_9.3.png)
10. 将系统中原有的nginx用重新编译生成的nginx文件替换，替换后重启nginx使新编译nginx生效
        # rm -rf /usr/local/nginx/sbin/nginx
        # cp objs/nginx /usr/local/nginx/sbin/
        # service nginx restart

 ![](/assets/Nginx filter_10.png)
11.  让云锁识别新编译的nginx

 1) 安装云锁，如已经安装则忽略此步骤。

 2) 编译nginx路径，使云锁识别
         # cd /usr/local/yunsuo_agent/nginx/
         # ./configure_compile_nginx /usr/local/nginx
 
 ![](/assets/Nginx filter_11.png)

12. 到此通过PC端连接到服务器端，在PC端的界面上可以看到已识别nginx插件。

 ![](/assets/Nginx filter_12.png)