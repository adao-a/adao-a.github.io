---
title: node项目部署到云服务器
date: 2023-03-17 22:40:12
---

轻部署,快应用

<!-- more-->
学习了*University of Helsinki: Full Stack open 2022*，其部署使用古老的`Heroku`来完成,但因不可抗原因无法使用，故选择了将作业直接部署到了腾讯云的服务器。

## ssh连接服务器

推荐使用`Xshell`,win自带的PoweShell不稳定

## 环境

- 安装node,npm

- 安装pm2: node进程管理工具,保证退出窗口后，node服务继续运行

- `Xftp1`: 文件传输

- 安装Nginx



## PM2

1. 使用npm全局安装pm2：
   ```
   npm install -g pm2
   ```

1. 启动：

   ```
   pm2 start app.js
   ```

3. 检查nodejs项目是否启动

   ```
   pm2 list
   ```

   

## Nginx反向代理

配置文件：/etc/nginx/nginx.conf

启动：/usr/sbin/  命令：./nginx

常用命令：

- start nginx：启动

- Nginx -T: 测试配置文件
- nginx -s reload:重启

配置：

```bash
server {
    listen    80 ipv6only=on ;
    server_name    47.115.213.35;//外网ip
    location /api/  {
            proxy_pass   http://172.31.46.134:3001;内网ip,node服务端口号
            }
    }
```
