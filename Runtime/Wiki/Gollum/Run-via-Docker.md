# Run via Docker
-
推荐使用Docker方式运行Gollum。

## Clone From Github

git@github.com:ushisoft/wiki.git

## 制作镜像
```
docker build -t gollum .
```
后续考虑将镜像上传至Docker仓库。

## 运行Docker
```
$ docker run -v `pwd`:/wiki -p 4567:4567 gollum
```
其中\`pwd`表示当前目录，运行Docker时务必cd到wiki所在目录。

## 参考
[Gollum Wiki](https://github.com/gollum/gollum/wiki/Gollum-via-Docker)
