```
docker pull biarms/mysql:5.7.33-beta-circleci
```

```
docker run -d \
    --name mysql \
    --restart always \
    -p 3306:3306 \
    -e MYSQL_ROOT_PASSWORD=adamodel@12 \
    -v /mnt/usb/opt/mysql:/var/lib/mysql \
    biarms/mysql:5.7.33-beta-circleci
```

```
version: '3.8'

services:
  mysql:
    image: biarms/mysql:5.7.33-beta-circleci
    container_name: mysql
    restart: always
    ports:
      - "3306:3306"
    environment:
      MYSQL_ROOT_PASSWORD: adamodel@12
    volumes:
      - /mnt/usb/opt/mysql:/var/lib/mysql
```

```
docker exec -it mysql /bin/bash
```

```
mysql -uroot -pyour_password
```

```
create user 'root'@'%' identified by 'adamodel@12';
```



---

```sh
docker run --name typecho-server -e TYPECHO_SITE_URL=http://ipv6.lamn.eu.org -d docker.adamo.dpdns.org/joyqi/typecho:nightly-php8.2-apache
```



---

# 玩客云 armv7l 架构安装 MySQL 5.7

由于 MySQL 官方未提供 armv7l 架构镜像，因此我们需要拉取第三方的 MySQL 镜像，例如本文用到的 [biarms/mysql](https://hub.docker.com/r/biarms/mysql/tags)

## 安装

### Docker

1. 拉取第三方镜像

```
docker pull biarms/mysql:5.7.33-beta-circleci
```

1. 运行 MySQL 容器

```
docker run -d \
    --name mysql \
    --restart always \
    -p 3306:3306 \
    -e MYSQL_ROOT_PASSWORD=your_password \
    -v /opt/mysql:/var/lib/mysql \
    biarms/mysql:5.7.33-beta-circleci
```

### Docker Compose

```
version: '3.8'

services:
  mysql:
    image: biarms/mysql:5.7.33-beta-circleci
    container_name: mysql
    restart: always
    ports:
      - "3306:3306"
    environment:
      MYSQL_ROOT_PASSWORD: your_password
    volumes:
      - /opt/mysql:/var/lib/mysql
```

## 开启外部访问

1. 进入容器

```
docker exec -it mysql /bin/bash
```

1. 进入 MySQL 命令行

```
mysql -uroot -pyour_password
```

1. 创建 MySQL 用户

```
create user 'root'@'%' identified by 'your_password';
```

1. 授予权限

```
grant all privileges on *.* to 'root'@'%' with grant option;
```

1. 刷新权限

```
flush privileges;
```

success



## 可能遇到的问题

### ERROR 3009

授予权限时，提示 `ERROR 3009 (HY000): Column count of mysql.user is wrong. Expected 45, found 42. Created with MySQL 50560, now running 50733. Please use mysql_upgrade to fix this error.`

表明 MySQL 数据库的用户表结构与当前版本的MySQL不匹配

执行以下代码即可解决

```sql
mysql_upgrade -uroot -pyour_password
```

---

```
docker run -d \
    --name certimate_server \
    --restart unless-stopped \
    -p 8090:8090 \
    -v /mnt/usb/certimate/data:/app/pb_data \
    registry.cn-shanghai.aliyuncs.com/usual2970/certimate:latest

```

```
docker run -d \
    --name mysql \
    --restart always \
    -p 3306:3306 \
    -e MYSQL_ROOT_PASSWORD=adamodel@12 \
    -v /mnt/usb/opt/mysql:/var/lib/mysql \
    biarms/mysql:5.7.33-beta-circleci
```

docker pull docker.adamo.dpdns.org/certimate/certimate:latest
