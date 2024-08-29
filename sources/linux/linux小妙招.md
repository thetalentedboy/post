---
title: 用DSL优化你的文档
description: 用DSL优化你的文档
ctime: 2024-08-24
---
## 服务器常用命令
```shell
#查看容器日志
docker logs -f <container-name>

#k8s查看pod日志
kubectl logs <pod>

#输出文件末尾几行的实时内容
tail -f log.txt

#log动态量大时使用, 可以用vim
vim log.txt

# 查看进程信息
ps aux | grep <pid/name>

# 查看端口占用
lsof -i :port

# 远端文件上传
scp -i test.pem ./index.txt  user@127.0.0.1:/usr/test/
```
