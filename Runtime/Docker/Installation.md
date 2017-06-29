# Docker的安装

## CentOS

```
sudo yum install -y yum-utils
```

```
sudo yum-config-manager --add-repo https://docs.docker.com/engine/installation/linux/repo_files/centos/docker.repo
```

```
sudo yum -y install docker-engine
```

注册Docker服务，保证机器重启时Docker能够运行：

```
sudo systemctl enable docker
```

## 权限
通过如下命令，将当前用户加入docker群组，即可在当前用户下执行docker命令：

```
sudo usermod -a -G docker $USER
```
