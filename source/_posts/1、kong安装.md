---
title: "1、kong安装"
date: "2023-06-05 16:13:00"
updated: "2023-06-08 18:27:00"
tags:
categories:
description: >-
  ### 一、配置网络 ```bash docker network create kong-net ``` ### 二、配置postgreSQL ```bash docker run -d --name kong-database \ --network=kong-net \ -p 5432:543
---

### 一、配置网络
```bash
docker network create kong-net
```

### 二、配置postgreSQL
```bash
 docker run -d --name kong-database \
  --network=kong-net \
  -p 5432:5432 \
  -e "POSTGRES_USER=kong" \
  -e "POSTGRES_DB=kong" \
  -e "POSTGRES_PASSWORD=kongpass" \
  postgres:13
```

### 三、初始化kong数据库
```bash
docker run --rm --network=kong-net \
 -e "KONG_DATABASE=postgres" \
 -e "KONG_PG_HOST=kong-database" \
 -e "KONG_PG_PASSWORD=kongpass" \
 -e "KONG_PASSWORD=test" \
kong/kong-gateway:3.3.0.0 kong migrations bootstrap
```
ps:
KONG_DATABASE: 指定 Kong 使用的数据库类型。
KONG_PG_HOSTkong-net：上一步中通过网络通信的 Postgres Docker 容器的名称 。
KONG_PG_PASSWORD：您在上一步中启动 Postgres 容器时设置的密码。
KONG_PASSWORD（仅限企业）：Kong Gateway 管理员超级用户的默认密码。
{IMAGE-NAME:TAG} kong migrations bootstrap：按顺序，这是 Kong Gateway 容器名称和标签，然后是 Kong 准备 Postgres 数据库的命令。

### 四、运行kong gateway
```bash
docker run -d --name kong-gateway \
 --network=kong-net \
 -e "KONG_DATABASE=postgres" \
 -e "KONG_PG_HOST=kong-database" \
 -e "KONG_PG_USER=kong" \
 -e "KONG_PG_PASSWORD=kongpass" \
 -e "KONG_PROXY_ACCESS_LOG=/dev/stdout" \
 -e "KONG_ADMIN_ACCESS_LOG=/dev/stdout" \
 -e "KONG_PROXY_ERROR_LOG=/dev/stderr" \
 -e "KONG_ADMIN_ERROR_LOG=/dev/stderr" \
 -e "KONG_ADMIN_LISTEN=0.0.0.0:8001" \
 -e "KONG_ADMIN_GUI_URL=http://localhost:8002" \
 -e KONG_LICENSE_DATA \
 -p 8000:8000 \
 -p 8443:8443 \
 -p 8001:8001 \
 -p 8444:8444 \
 -p 8002:8002 \
 -p 8445:8445 \
 -p 8003:8003 \
 -p 8004:8004 \
 kong/kong-gateway:3.3.0.0
```
ps:
--nameand --network：要创建的容器的名称，以及它所通信的 Docker 网络。
KONG_DATABASE: 指定 Kong 使用的数据库类型。
KONG_PG_HOST：通过网络通信的 Postgres Docker 容器的名称 kong-net。
KONG_PG_USERandKONG_PG_PASSWORD : Postgres 用户名和密码。Kong Gateway 需要登录信息来将配置数据存储在KONG_PG_HOST数据库中。
所有_LOG 参数：设置日志输出到的文件路径，或使用示例中的值将消息和错误打印到stdout和stderr。
KONG_ADMIN_LISTEN：Kong Admin API 监听请求的端口。
KONG_ADMIN_GUI_URL：（仅限企业）用于访问 Kong Manager 的 URL，前面带有协议（例如，http://）。
KONG_LICENSE_DATA：（仅限企业）如果您有许可证文件并将其保存为环境变量，则此参数会从您的环境中提取许可证。

### 五、验证
gateway是否可用：
```bash
curl -i -X GET --url http://localhost:8001/services
```

管理端地址：http://localhost:8002

### 六、不需要就清理
```bash
docker kill kong-gateway
docker kill kong-database
docker container rm kong-gateway
docker container rm kong-database
docker network rm kong-net
```
