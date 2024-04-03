# 环境和工具
- Ubuntu 20: 操作系统
- Docker & Docker Compose: 部署和运行环境，容器编排
- Jenkins: 开源CI&CD, 构建伟大，无所不能
- Zentaopms: 禅道项目管理/文档 [docker compose yaml](./TOOLS-zentao.md)
- Bandicam: 录视频录教程，备用（OBS，Captura，ApowerREC，QQ，Win+G快捷键，N卡录制）
- github: 代码仓库/代码管理， [仓库地址](https://github.com/chipabs)
 
# OS
- ubuntu 20
  - Linux ideaSoft 5.15.0-97-generic #107~20.04.1-Ubuntu SMP Fri Feb 9 14:20:11 UTC 2024 x86_64 x86_64 x86_64 GNU/Linux
- openjdk-8-jdk
  - /usr/lib/jvm/java-1.8.0-openjdk-amd64

## Jenkins
- 构建伟大，无所不能
- Jenkins是开源CI&CD软件领导者， 提供超过1000个插件来支持构建、部署、自动化， 满足任何项目的需要。
  - 持续集成和持续交付: 作为一个可扩展的自动化服务器，Jenkins 可以用作简单的 CI 服务器，或者变成任何项目的持续交付中心。
  - 简易安装: Jenkins 是一个基于 Java 的独立程序，可以立即运行，包含 Windows、Mac OS X 和其他类 Unix 操作系统。
  - 配置简单: Jenkins 可以通过其网页界面轻松设置和配置，其中包括即时错误检查和内置帮助。
  - 插件: 通过更新中心中的 1000 多个插件，Jenkins 集成了持续集成和持续交付工具链中几乎所有的工具。
  - 扩展: Jenkins 可以通过其插件架构进行扩展，从而为 Jenkins 可以做的事提供几乎无限的可能性。
  - 分布式: Jenkins 可以轻松地在多台机器上分配工作，帮助更快速地跨多个平台推动构建、测试和部署。
- [文档中心 https://www.jenkins.io/zh/doc/](https://www.jenkins.io/zh/doc/)
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
  - [docker-compose.yaml](./TOOLS-jenkins-docker-compose.yaml)
  - 账户信息: jadmin/Ken123



## Zentaopms
- 专业的研发项目管理软件
  - [zentao安装说明](./TOOLS-zentao.md)
  - 账户信息: zentaoadmin/Ken123
