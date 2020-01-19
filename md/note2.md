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

## DockerFile 体系结构汇总
- FROM     
  基础镜像，当前镜像是基于那个镜像的

- MAINTAINER
  当前镜像维护者姓名或者邮箱等信息

- RUN 
  在容器构建时指定需要运行的命令
 
- EXPOSE 
  当前容器需要对外暴露的端口
  
- WORKDIR
  指定创建容器后，终端默认登录进来的工作目录，一个落脚点，相当与linux下的cd命令
 
- ENV 
  用来在构建镜像过程中设置环境变量
  
- ADD
  将宿主机目录下的文件拷贝进镜像且ADD命令会自动处理URL和解压tar压缩包
  
- COPY
  类似ADD，拷贝文件和目录到镜像中，和ADD类似，不含解压功能
  
- VOLUME 
  容器数据卷，用于数据保存和持久化工作
  
- CMD
  指定一个容器启动时要运行的命令  
  **注意**：Dockerfile中可以有多个CMD命令，但是最后只有一个生效，CMD会被docker run 之后的参数替换
  
- ENTRYPOINT
 指定一个容器启动时要运行的命令，目的和CMD一样，都是在指定容器启动程序和参数
 
- ONBUILD: 
当构建一个被继承的Dockerfile时运行时命名，父镜像在被子镜像继承后父镜像的onbuild被触发。


  



