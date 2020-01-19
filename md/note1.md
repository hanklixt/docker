### docker 入门使用
## 安装启动
-  安装docker
```
 # 安装docker官方源
sudo yum-config-manager \
--add-repo \
https://download.docker.com/linux/centos/docker-ce.repo
# 如提示 yum-config-manager: command not found 做如下操作
 yum install -y yum-utils
#更新源
yum makecache fast

#下载
yum install docker-ce

```

- 设置开机启动
```
systemctl enable docker
```
 
- 启动docker
```
systemctl start docker
```

- 停止docker
 
```
systemctl stop docker

```

- 重启docker

```
systemctl restart docker
```
 

## 镜像操作

- 搜索镜像

```
#根据服务名进行搜索
docker search servicename

```


- 下载镜像
  
```
#镜像名:版本号   下载对应版本镜像
docker pull name:tag

# 镜像名  下载最新的镜像版本
docker pull name

```

- 查看本地所有已下载镜像
 
```
docker images
```

- 删除镜像
```
#根据镜像id删除
docker rmi imageid

# 根据镜像id强制删除，不带-f需要先删除容器，再删除镜像
docker rmi -f  imageid

# 删除所有镜像 ，相关与mysql in +字句查询，提取所有的镜像id进行删除
docker rmi -f $(docker image -qa)

```

- 查看镜像摘要信息
```
# 查看摘要信息
docker images --digests -a
```

## 容器操作

- 端口操作
  
```
#使用镜像后台运行容器 指定容器名  指定启动方式   指定宿主机端口:容器暴露端口      镜像名
docker run   --name  test-nginx         -d              -p 8080:80                             nginx

#端口映射
-p 80:80
# 端口批量映射
-p 80-90:80-90


```

- 端口操作补充说明
**-d:后台运行容器 ，并返回容器id,也即启动守护式容器
-i:以交互模式运行容器
-t:为容器重新分配一个伪输入终端，通常与-i同时使用**

```
docker run -d -it 镜像名
```

- 查看容器运行状态
  
```
docker ps [option]
#列出所有正在运行的容器+历史上运行过的
docker ps -a     
# 列出上一个运行的容器
docker ps -l     
#  列出上一个运行的容器 只显示id
docker ps -lq

```

- 容器重启删除等操作
```
#根据容器id重启容器
docker restart   containerId

#根据容器id启动容器
docker start containerid

#根据容器id停止容器
docker stop containerid 
docker kill containerid 

#根据容器id强制删除，不加-f 先停止，再删除
docker rm -f  containerid  

#强制一次性删除所有容器
docker rm -f $(docker ps -a -q)

```

- 查看容器内进程
 
```
#查看容器内部进程
docker top 容器id

```

- 查看容器内部细节
```
docker inspect  容器id
```

- 把容器内文件拷贝到目标主机
```
docker cp 容器id:容器内文件路径 宿主机目录
```

- 容器挂载目录
```
#运行容器   挂载  宿主机目录：容器目录           镜像
docker run  -v    data:/usr/share/nginx/html  nginx
```

## 日志操作

-  查看日志
```
#查看r容器内日志
 docker logs containerid
 
 #一直追加查看最新的日志
 docker logs -f containerid
 #一直追加查看最新的日志同时加入时间戳
 docker los  -f  -t  containerid
 #查看倒数第100行内日志
 docker logs --tail  100
```


