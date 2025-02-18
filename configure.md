# nginx 配置文件

安装好的 nginx 主配置文件位于`/etc/nginx/nginx.conf`，可以直接修改其中的配置项

- `nginx -V`查看配置文件地址
- `nginx -t`修改配置文件后检查配置文件是否存在语法错误
- `nginx -c [filename]`指定配置文件

以下是一个最小的配置模板：

```nginx
# nginx模型为一个 master 进程管理多个 worker 进程，由 worker 进程处理访问请求
# worker_processes 选项用以指定进程数，通常设置成和cpu的数量相等
worker_processes auto;

# 事件驱动模块，设置工作模式及连接数上限
events {
    # 单个后台 worker 进程的最大并发链接数
	worker_connections 768;
}

# http服务器模块，利用它的反向代理功能提供负载均衡支持
http {
    # 设定mime类型，由mime.types文件定义，并制定默认type
	include /etc/nginx/mime.types;
	default_type application/octet-stream;

    # 指定 nginx 是否调用 sendfile 函数（zero copy 方式）来输出文件
    sendfile on;

    # 连接超时时间
    keepalive_timeout 65;

    # http服务器
    server {
        # 监听80端口
        listen 80;
        listen [::]:80;

        # 定义使用访问的地址，可以直接填入域名
        server_name  localhost;

        # 反向代理的路径，location 后面设置映射的路径
        location / {
            root   /usr/share/nginx/html;
            index  index.html index.htm;
        }
    }
}
```
