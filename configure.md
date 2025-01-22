# nginx 配置文件

安装好的 nginx 主配置文件位于`/etc/nginx/nginx.conf`，可以直接修改其中的配置项。也可通过指令`nginx -V`查看配置文件地址，每次修改配置文件后可以通过`nginx -t`检查配置文件是否存在语法错误。

```nginx
worker_processes auto;   # nginx模型为一个master进程管理多个worker进程，由worker进程处理访问请求

# 事件驱动模块
events {
	worker_connections 768;
}

http {
	include /etc/nginx/mime.types;
	default_type application/octet-stream;

    sendfile on;

    keepalive_timeoue 65;

	server {
        listen 80 default_server;
        listen [::]:80 default_server;

        root /var/www/html;

        server_name _;

        location / {
            try_files $uri $uri/ =404;
        }
    }
}
```
