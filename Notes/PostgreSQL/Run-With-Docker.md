# Run With Docker

## 版本

`docker pull postgres:10.5`

## 运行

`docker run --name postgres1 -e POSTGRES_PASSWORD=password -p 5432:5432 -d postgres:10.5`