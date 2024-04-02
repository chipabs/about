# 环境和工具
- Ubuntu 20: 操作系统
- Docker & Docker Compose: 部署和运行环境，容器编排
- Jenkins: 开源CI&CD, 构建伟大，无所不能
- Redmine: 项目管理，文档
- Bandicam: 录视频录教程，备用（OBS，Captura，ApowerREC，QQ，Win+G快捷键，N卡录制）

 
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


## Redmine
- Redmine 是一个灵活的项目管理 web 应用程序。它使用 Ruby on Rails 框架编写，是跨平台和跨数据库的。
- Redmine 是开源的，根据 GNU 通用公共许可证v2（GPL）的条款发布。
- 功能特点
  - 支持多个项目、子项目
  - 灵活的基于角色的访问权限控制
  - 灵活的问题跟踪系统
  - 甘特图和日历
  - 新闻、文档和文件管理
  - 提要和电子邮件通知
  - 项目中可添加 Wiki
  - 项目中可添加论坛
  - 任务工时跟踪
  - 可为问题、耗时、项目、版本、文档、用户组、活动（时间跟踪）、问题优先级等增加自定义字段
  - SCM集成（SVN、CVS、Git、Mercurial 和 Bazaar）
  - 支持通过电子邮件创建问题
  - 支持多个 LDAP 身份验证
  - 支持用户自主注册
  - 支持多种语言
  - 支持多种类型数据库
- Redmine安装
```
version: '3.1'
services:
  postgres:
    image: postgres:latest
    restart: always
    networks:
      - redmine
    volumes:
      - /home/<your_path_here>/data/postgres-data:/var/lib/postgresql/data
    environment:
      - 'POSTGRES_PASSWORD=<your_password_here>'
      - 'POSTGRES_DB=redmine'
  redmine:
    image: redmine:latest
    restart: always
    networks:
      - redmine
    volumes:
      - /home/<your_path_here>/data/redmine-data:/usr/src/redmine/files
    ports:
      - 10080:3000
    environment:
      - 'REDMINE_DB_POSTGRES=postgres'
      - 'REDMINE_DB_DATABASE=redmine'
      - 'REDMINE_DB_PASSWORD=<your_password_here>'
volumes:
  postgres-data:
  redmine-data:
networks:
  redmine:
    driver: bridge
```
