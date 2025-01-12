# 安装 nginx

本次采用了最简易的包管理器安装，在 Ubuntu 上采用了`apt-get`命令

```shell
sudo apt-get update
sudo apt-get install nginx
```

### 启动 nginx

安装后，Nginx 应该会自动启动。但是，如果安装后未启动该服务，可以运行以下命令来启动该服务。

```shell
sudo systemctl start nginx
```

可以使用以下命令检查 Nginx 的状态

```shell
sudo systemctl status nginx
```

如果启动 Nginx 服务时出现错误，很有可能是 80 端口已被使用。Nginx 默认使用端口 80 进行 HTTP 流量。如果另一个服务已经使用了 80 端口，Nginx 将无法启动。要检查 80 端口是否被使用，可以运行以下命令

```shell
sudo lsof -i :80
```

### nginx 服务控制

在一般的环境中，输入`nginx`即可启动服务，服务启动后会自动分配到 80 端口。启动后可以通过`nginx -s [signal]`来传递指令，包括：

- `quit`：优雅停止
- `exit`：立即停止
- `reload`：重新加载配置文件
- `reopen`：重新打开日志文件
