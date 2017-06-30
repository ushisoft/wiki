# Run via Docker

使用Docker方式运行Shadowsocks。

## 运行Docker

使用第三方镜像即可:

```sh
docker run -d -p 54285:54285 oddrationale/docker-shadowsocks -s 0.0.0.0 -p 54285 -k password -m aes-256-cfb
```

