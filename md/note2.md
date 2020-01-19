### Dockerfile 常用指令并上传DockerHub流程
## 示例代码1
```
#继承官方的centos镜像
FROM centos

#容器元信息，帮助信息，metaData,类似于代码注释
LABEL version="1.0"


#每条指令后构建一层对于复杂的RUN命令，为了避免无用的分层，多条命令用反斜线换行，合成一条命令！
RUN yum update && yum install -y vim  \
yum install  -y vi

#相当于linux的cd命令，改变目录，尽量使用绝对路径！！，不要用RUN  cd

WORKDIR  /root
#如果没有这个目录，会自动创建
WORKDIR /test   

#添加到目录并且解压
ADD test.tar.gz  /  
#添加到工作目录
COPY hello test
# ADD 与COPY  ADD 除了COPY 功能外还有解压功能
#配置环境变量  尽可能使用ENV 增加可维护性
ENV 
ENV MYSQL_VERSION 5.7

```

## 示例代码2
 
```
#指定父镜像
 FROM nginx
 
#配置环境变量  字符集 
ENV LANG en_US.UTF-8
#拷贝当前目录index.html文件到容器指定目录
ADD  index.html  /usr/share/nginx/html
#暴露端口
EXPOSE 80
EXPOSE 443



```

## 构建镜像
```
#                        镜像名称：tag版本
docker build  .  -t  hello-test:0.0.1
```
## 上传镜像到dockerhub
-  登录([dockerhub地址](https://hub.docker.com))

```
#注册操作完成后，在linx上登录
docker login
```

- 编辑要上传的镜像

```
 #                                 仓库名/镜像名称:tag版本
docker tag hello-lxt:0.0.1 hankbaba/hello-lxt:0.0.1
```

-推送镜像

```
docker push hankbaba/hello-lxt:0.0.1
```

- 测试
```
#删除本地镜像
docker rmi -f hankbaba/hello-lxt:0.0.1
#从dockerhub上拉取
docker pull hankbaba/hello-lxt:0.0.1

```








