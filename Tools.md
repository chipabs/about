# 环境和工具

# OS
- ubuntu 20
  - Linux ideaSoft 5.15.0-97-generic #107~20.04.1-Ubuntu SMP Fri Feb 9 14:20:11 UTC 2024 x86_64 x86_64 x86_64 GNU/Linux
- openjdk-8-jdk
  - /usr/lib/jvm/java-1.8.0-openjdk-amd64

## Jenkins
- Docker Installation

```
docker pull jenkinsci/blueocean

mkdir -p /usr/local/jenkins
chmod 777 /usr/local/jenkin

# -d 后台方式启动
# -p 映射端口，宿主机端口:容器内端口
# -v 挂载卷，将容器Jenkins工作目录/var/jenkins_home挂载到宿主机目录/usr/local/jenkins
# -name 给容器起个别名
docker run -d -p 8099:8080 -p 50099:50000 -v /usr/local/jenkins:/var/jenkins_home --name myjenkins jenkinsci/blueocean

[root@chenpihost local]# docker ps
CONTAINER ID   IMAGE                 COMMAND                  CREATED          STATUS          PORTS                                                                                      NAMES
538de1b1b1f5   jenkinsci/blueocean   "/sbin/tini -- /usr/…"   18 seconds ago   Up 17 seconds   0.0.0.0:8099->8080/tcp, :::8099->8080/tcp, 0.0.0.0:50099->50000/tcp, :::50099->50000/tcp   myjenkins
```

- docker compose up -d

```
services:
  jenkins:
    image: "jenkins/jenkins:lts-jdk17"
    #image: "jenkinsci/blueocean:latest"
    user: "root"
    privileged: "true"
    restart: "always"
    container_name: "jenkins"
    volumes:
      - /usr/local/jenkins:/var/jenkins_home
      - /var/run/docker.sock:/var/run/docker.sock
      - /usr/bin/docker:/user/bin/docker
      - /usr/lib/x86_64-linux-gnu/libltdl.so.7:/usr/lib/x86_64-linux-gnu/libltdl.so.7
      - /etc/docker/daemon.json:/etc/docker/daemon.json
      - /usr/lib/jvm/java-1.8.0-openjdk-amd64:/usr/local/java/jdk1.8.0_161
    ports:
      - "8080:8080"
      - "50000:50000"

```

- 账户信息
  - jadmin/Ken123