# Run via Docker

使用Docker方式运行Shadowsocks。

## 运行Docker

使用第三方镜像即可

```
docker run -d -p 54285:54285 oddrationale/docker-shadowsocks -s 0.0.0.0 -p 54285 -k 34qRqvRa -m aes-256-cfb
```
