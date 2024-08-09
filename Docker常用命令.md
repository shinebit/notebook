# Docker常用命令

## 镜像
#### 查询镜像
```shell
# 查询本机的所有镜像，并显示详细信息
docker images
```
#### 获取镜像
```shell
# 拉取最新的镜像版本
docker pull 镜像名

# 拉取指定版本镜像
docker pull 镜像名:tag
```
#### 删除镜像
```shell
# 删除指定镜像
docker rmi 镜像名/镜像ID

# 强制删除
docker rmi -f 镜像名/镜像ID
```

## 容器
#### 查询容器
```shell
# 查询当前正在运行的容器
docker ps

# 查询所有存在的容器，包括已退出的
docker ps -a
```
#### 启动容器
```shell
# 启动容器
docker run 参数

# 停止正在运行容器
docker stop 容器名/容器ID

# 启动已经停止的容器
docker start 容器名/容器ID

# 重启容器
docker restart 容器名/容器ID
```
#### 进入容器
```shell
# 进入当前运行容器，并创建一个新的交互式界面
docker exec -it 容器名/容器ID /bin/bash

# 退出容器至后台快捷键
ctrl+p+q
```
#### 删除容器
```shell
# 删除已退出的容器
docker rm 容器名/容器ID

# 强制删除容器，包括正在运行的
docker rm -f 容器名/容器ID
```

## Docker Compose
```shell
# 创建并后台运行容器
docker-compose up -d

# 创建并后台运行指定模板容器
docker-compose -f docker-compose.yml up -d
```
