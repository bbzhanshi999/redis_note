部署步骤

1.将springboot项目打包
2.在linux创建一个文件夹docker_compose_app,
3.将jar包放入文件夹
4.在文件夹查下创建dockerfile
5.编辑dockerfile

```dockerfile

# 基础镜像
from openjdk:8-jdk-alpine
# 拷贝jar包到镜像某一个位置下
COPY redis-demo-0.0.1-SNAPSHOT.jar /app.jar
# 运行启动命令
CMD ["java","-jar","/app.jar","--spring.redis.host=redis"]

```

6.编辑docker-compose.yml

```yaml
version: '3'
services:
	redis-demo:
		build: .     #指定Dockerfile的位置
		ports:
		  - "8080:8080"
	redis:
		image: "redis"   #指定redis服务的镜像，也就是创建容器对应的镜像
```

7.在docker_compose_app文件夹下执行命令

```bash
docker-compose up  
#这行命令在有docker-compose.yaml的文件夹下执行
```



docker-compose命令：

1.创建镜像，下载镜像

2.创建了供多个容器进行互联虚拟网络环境

3.启动容器