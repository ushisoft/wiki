# Run

## Run Via Docker

### Install Docker

```sh
# 安装工具包，yum-utils包含yum-config-manager等使用工具
yum install -y yum-utils \ device-mapper-persistent-data \ lvm2
# 添加yum源
yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
# 安装docker
yum install -y docker-ce
# 配置docker自启动
systemctl enable docker
# 启动docker
systemctl start docker
# 验证docker，hello-world是官方最小镜像
docker run hello-world
```

edge和test库可选：

```sh
yum-config-manager --enable docker-ce-edge
yum-config-manager --enable docker-ce-test
```

### Run

```sh
# 运行SS，相应的修改端口和密码等信息
docker run -e PASSWORD=password -e METHOD=aes-256-gcm -p 8388:8388 -d --restart always shadowsocks/shadowsocks-libev
```

## Run Via Docker-Compose (Optional)

### Download File From Github

```sh
mkdir -p ~/shadowsocks/
cd ~/shadowsocks/
# 从github处下载模板
curl -sSLO https://github.com/ushisoft/docker-compose-files/raw/master/SS/docker-compose.yml
# 修改端口、密码等基本信息后执行，其他环境变量可参考https://github.com/shadowsocks/shadowsocks-libev/blob/master/docker/alpine/README.md
docker-compose up -d
docker-compose ps
```

