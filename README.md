# sub-web

> 基于 vue-cli 与 [subconverter](https://github.com/tindy2013/subconverter) 后端实现的订阅转换。

## 环境要求

需要 [Node](https://nodejs.org/zh-cn/) 与 [Yarn](https://legacy.yarnpkg.com/en/docs/install) 来安装依赖与打包发布，可以通过以下命令查看是否安装成功。

```shell
node -v
yarn -v
```

## 安装

```shell
yarn install
```

## 使用

```shell
yarn serve
```

浏览器访问 <http://localhost:8080/>

## 发布

执行以下打包命令，生成的 dist 目录即为发布目录。

```shell
yarn build
```

你需要安装 nginx (或其他 web 服务器)并正确配置，以下为示例配置：

```shell
server {
    listen 80;
    server_name sub.343.re;
    return 301 https://$server_name$request_uri;
}

server {
    listen 443 ssl http2;
    server_name sub.343.re;
    ssl_certificate /etc/ssl/certs/343.re/fullchain.pem;
    ssl_certificate_key /etc/ssl/certs/343.re/privkey.pem;
    root /var/www/sub-web/dist;
    index index.html;
    error_page 404 /index.html;

    gzip on;
    gzip_min_length 1k;
    gzip_buffers 4 16k;
    gzip_http_version 1.0;
    gzip_comp_level 6;
    gzip_types text/plain text/css text/javascript application/json application/javascript application/x-javascript application/xml;
    gzip_vary on;

    location ~* \.(css|js|png|jpg|jpeg|gif|gz|svg|mp4|ogg|ogv|webm|htc|xml|woff)$ {
        access_log off;
        add_header Cache-Control "public,max-age=30*24*3600";
    }
}
```

## 许可证

MIT © 2020 Dnomd343 (fork from CareyWang)
