
# 安装
``` bash
#arch linux
sudo pacman -S docker
```

# 开始之前
``` shell
sudo systemctl start docker

# 自启
sudo systemctl enable docker 

# 为当前用户添加添加控制组
sudo usermod -aG docker $user
```

# 常规命令
``` shell
# 查看所有启动中的容器
docker ps 

# 查看所有容器启动记录， 我们可以通过docker start命令， 使用记录中曾经的<container-id> ，启动一个和曾经相同的容器， 但是不能重新赋予启动命令。
docker ps --all

# 创建容器, command为在容器中执行的命令
docker create <image-name> <command>
#output <container-id> dawdhawdsadakdwaodawjodjwoadjwaidjawd

# 启动容器
docker start <container-id>

# docker run = docker create + docker run
docker run <image-name> <command>

# 查看某个container log
docker logs <container-id>

# 卸载全部container
docker system prune

# 停止, 与立即停止不同的是 他回往容器内发送消息，他说你要停止了，然后容器内可以执行一些回调触发事件什么的， 如果容器内没有对停止的消息做出响应，那么十秒种之后会杀掉这个进程。
docker stop <container-id>

# 立即停止, 立即杀掉进程，对付无法关闭的，出现故障的容器可以使用。
docker kill <container-id>

# 向容器中追加命令, 
#-i: 将现有的终端与容器连接，就好像和他ssh了一样只是一个比喻。
#-t: 对终端的输入输出进行格式化。
docker exec -it <container-id> <command>

# example: 操作指定容器内的tty
docker exec -it <container-id> sh

# example: 我想很快的启动并且进入他的sh
docker run -it <image-name> sh
```

# Dockerfile
```shell
# use Alpine Linxu image as container base 
FROM alpine

# alpine install redis
RUN apk add --update redis

# container tty command
CMD ["redis-server"]
```

流程解析：
1. FROM： 拉取alpine镜像，并生成一个临时镜像。
2. RUN: 可能有很多步，每次执行的时候会基于上一步生成的镜像，run 一个临时容器，执行命令后退出。 
    
    tips: 尽量少的使用RUN, 能用一行写完就写完， 因为会产生更多的step。
        
3. CMD: 基于最后生成的镜像， 附加启动命令

手动实现：
上述流程使用命令实现，让你更加理解dockerfile build 的过程，但是不建议这样做，更加建议使用Dockerfile.
```shell
 # run alpins image
docker run -it alpine sh

# 下载依赖redis
/ apk add --update redis
# 退出容器
/ exit

# 拿到刚刚的容器ID
docker ps --all

# 修改容器启动后执行的命令，这样我们就能得到一个新的容器，实现了dockerfile的效果。
# commit 基于已经运行的容器创建一个新的镜像  -c 设置这个镜像的CMD
docker commit -c 'CMD ["redis-server"]' <container-id>
```

# Get started
搭载一个简单的项目，
目录如图
``` shell
├── Dockerfile
├── index.js
├── package.json
└── package-lock.json
```

Dockerfile
```shell
# base image
FROM node:alpine

COPY . /usr/app
WORKDIR /usr/app

EXPOSE 8888

RUN cd /usr/app && npm install

CMD [ "npm", "start" ]
```

- FROM: base image 选用了node:alpine, 即nodejs镜像最简易版本，其中预置了node和npm。
- COPY: 第一个参数是要copy进容器的文件夹，第二个参数是把copy的文件夹放在容器的哪里。
- EXPOSE: 这个参数表明，我在内部可能会使用这个端口，方便宿主机器运维， 查看需要暴漏哪些端口给外部（maybe）， 比如上述例子中npm start 就会启动一个服务，监听端口为8888
- CMD: 基于最后生成的镜像， 附加启动命令


```shell
docker run -p 8080:8888 <localhost-port>:<container-port> hexw/express-project
```
- -p 8080:8888 : 将宿主机的8080 映射到容器中的8888， 如果你想暴漏多个端口那么可以重复这个命令， 但是微服务架构通常更倾向于将一个服务放在一个容器中，即一个服务一个容器。这种做法被称为"单一服务容器化"（Single-Service Containerization）或"微服务容器化"（Microservice Containerization）。
