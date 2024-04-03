## 网址
- [禅道20.0.beta2发布啦，修复Bug，提升系统稳定性](https://www.zentao.net/dynamic/20.0.beta2-83490.html)

## compose.yaml

```
# docker-compose.yaml
#version: '2'
services:
# db service for zentao
  zentao-db:
    image: bitnami/mariadb
    container_name: zentao-db
    ports:
      - '3306:3306'
    volumes:
      - /usr/local/zentao/mysql-data:/bitnami/mariadb
    environment:
      - MARIADB_ROOT_PASSWORD=pass4Zentao
      - MARIADB_DATABASE=zentao
    networks:
      - zentao-net
# zentao service
  zentao:
    image: hub.zentao.net/app/zentao
    container_name: zentao
    ports:
      - '8081:80'
    volumes:
      - /usr/local/zentao/file:/data
    depends_on:
      - zentao-db
    environment:
      - ZT_MYSQL_HOST=zentao-db
      - ZT_MYSQL_PORT=3306
      - ZT_MYSQL_USER=root
      - ZT_MYSQL_PASSWORD=pass4Zentao
      - ZT_MYSQL_DB=zentao
      - PHP_MAX_EXECUTION_TIME=120
      - PHP_MEMORY_LIMIT=512M
      - PHP_POST_MAX_SIZE=128M
      - PHP_UPLOAD_MAX_FILESIZE=128M
      - LDAP_ENABLED=false
      - SMTP_ENABLED=false
      - APP_DEFAULT_PORT=80
      - APP_DOMAIN=zentao.demo.com
      - PROTOCOL_TYPE=http
      - IS_CONTAINER=true
      - LINK_GIT=false
      - LINK_CI=false
    networks:
      - zentao-net
networks:
  zentao-net:
    driver: bridge

```