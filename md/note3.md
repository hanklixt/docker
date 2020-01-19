### 使用docker 构建springboot应用
##  Dockerfile示例代码
- 编写DockerFile(准备好springboot jar 项目)

```
#指定父镜像
FROM java:8
#创建/tmp目录并且持久化到Docker数据文件夹，因为SpringBoot使用的内嵌tomcat容器默认使用/tmp作为工作目录  
VOLUME /tmp
#拷贝宿主机当前目录指定文件到容器
ADD hello.jar hello.jar
#指定暴露的端口
EXPOSE 8080

# -Djava.security.egd=file:/dev/./urandom这个参数是加快启动时间
ENTRYPOINT  ["java","-Djava.security.egd=file:/dev/./urandom"], "-jar" ,"/hello.jar"]

```

## 构建镜像
```                      
                          #镜像名称:tag版本
  docker build . -t   hello:0.0.1
```


## 根据制作的镜像运行容器服务
```
docker run -d -p 8080:8080 --name hello  hello:0.0.1
```