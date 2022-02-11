
## 构建 在根目录运行（首次构建会比较慢）
docker-compose up -d

## 查看 镜像
docker images

## 查看 运行中的容器
docker ps 
> 查看所有容器 docker pa -a

## 停止容器
docker stop 容器id

## 重启容器
docker restart 容器id

## 删除容器
docker rm 容器ID
> 必须要 先停止 才能删除

## 进入容器
docker exec -it 容器ID /bin/bash
> 进入容器相当于进入对应的 linux 系统
