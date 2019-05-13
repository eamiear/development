# NGINX 基础配置

```bash
#user  nobody nobody;   # 配置用户或组
worker_processes  1;    # 允许生成的进程数，默认1。通常设置和cpu数量相等

#error_log  logs/error.log;             # 日志存储路径
#error_log  logs/error.log  notice;     # 制定日志储存路径及级别
#error_log  logs/error.log  info;

#pid        logs/nginx.pid;     # 制定 nginx 进程运行文件（PID）存放地址


events {
    #accept_mutex on;            # 设置网络连接序列化，防止惊群现象发生，默认为on
    #multi_accept on;            # 设置一个进程是否同时接受多个网络连接，默认为off
    #use epoll;                  # 事件驱动模型， select|poll|kqueue|epoll（多路复用IO）|resig|/dev/poll|eventport
    worker_connections  1024;    # 最大连接数，默认为 512
}


http {
    include       mime.types;    # 文件拓展名与文件类型映射表
    default_type  application/octet-stream; # 默认文件类型，默认为text/plain

    # 自定义日志格式
    #log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
    #                  '$status $body_bytes_sent "$http_referer" '
    #                  '"$http_user_agent" "$http_x_forwarded_for"';

    #access_log off;    # 取消服务日志
    #access_log  logs/access.log  main; # 设置日志格式为 main 类型（log_format中定义），默认为 combined

    sendfile        on; # 运行sendfile方式传输文件，默认为off， 可以在http块，server块，location块中配置
    
    #sendfile_max_chunk 100k;   # 每个进程每次调用传输数量不能大于设定的值，默认为0，即不设上限

    #tcp_nopush     on;

    #keepalive_timeout  0;  # 连接超时时间，默认为75s， 可以在http，server，location模块进行配置
    keepalive_timeout  65;

    #gzip  on;  # 开启gzip压缩

    # 设置请求缓冲
    #client_header_buffer_size 128k;
    #large_client_header_buffers 4 128k;

    # 设定虚拟主机配置
    server {
        listen       80;        # 监听80端口
        server_name  localhost; # 设置服务名称，访问路径

        #root html;             # 定义服务器的默认网站根目录位置

        #charset koi8-r;

        #access_log  logs/host.access.log  main;    # 设定本虚拟主机的访问日志

        # 默认请求
        location / {
            root   html;    # 请求目录位置
            index  index.html index.htm;    # 首页索引文件的名称
        }

	

        # 定义错误提示页面
        #error_page  404              /404.html;

        # redirect server error pages to the static page /50x.html
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }

        # 静态文件，nginx自己处理
        location ~ ^/(images|javascript|js|css|flash|media|static)/ {
            
            #过期30天，静态文件不怎么更新，过期可以设大一点，
            #如果频繁更新，则可以设置得小一点。
            expires 30d;
        }

        # proxy the PHP scripts to Apache listening on 127.0.0.1:80
        #
        #location ~ \.php$ {
        #    proxy_pass   http://127.0.0.1;
        #}

        # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
        #
        #location ~ \.php$ {
        #    root           html;
        #    fastcgi_pass   127.0.0.1:9000;
        #    fastcgi_index  index.php;
        #    fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;
        #    include        fastcgi_params;
        #}

        # deny access to .htaccess files, if Apache's document root
        # concurs with nginx's one
        #
        #location ~ /\.ht {
        #    deny  all;
        #}
    }


    # another virtual host using mix of IP-, name-, and port-based configuration
    #
    #server {
    #    listen       8000;
    #    listen       somename:8080;
    #    server_name  somename  alias  another.alias;

    #    location / {
    #        root   html;
    #        index  index.html index.htm;
    #    }
    #}


    # HTTPS server
    #
    #server {
    #    listen       443 ssl;
    #    server_name  localhost;

    #    ssl_certificate      cert.pem;
    #    ssl_certificate_key  cert.key;

    #    ssl_session_cache    shared:SSL:1m;
    #    ssl_session_timeout  5m;

    #    ssl_ciphers  HIGH:!aNULL:!MD5;
    #    ssl_prefer_server_ciphers  on;

    #    location / {
    #        root   html;
    #        index  index.html index.htm;
    #    }
    #}

}

```