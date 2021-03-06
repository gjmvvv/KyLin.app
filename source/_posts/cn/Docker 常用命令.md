---
title: Docker 常用命令
iscopyright: true
comments: true
lang: cn
tags:
  - docker
  - command
categories:
  - docker
abbrlink: docker
date: 2019-08-11 16:46:03
---


- apt-cache madison docker-ce 查看那些版本
- sudo apt-get install docker-ce=<VERSION> 安装指定版本

- docker images：查看已经安装的 docker 镜像。
- docker image rm image_id：删除镜像。
- docker pull：获取镜像。
- docker search：从仓库查找镜像文件。
- docker exec –it fID bash：进入 docker 容器内部。 
- docker exec -it dockermysql bash 进入容器内部
    - 注意事项
        1. 在windows 报错
            ```
                the input device is not a TTY.  If you are using mintty, try prefixing the command with 'winpty'
            ```
            - 解决方案: 命令前加 winpty 执行
        2. exit 退出

- docker run：运行 docker 镜像。
- docker ps：查看运行容器进程。
- docker run –d：在后台运行 docker 镜像。
- docker run –p：3306:3306 端口映射。
- docker stop ID：停止正在运行的容器。
 

- 添加一个 docker network 
``` docker
    docker network create nginx-proxy
```



---
## Docker-Mysql

- 命令说明：
    ```
        -p 3306:3306：将容器的 3306 端口映射到主机的 3306 端口
        -v -v $PWD/conf:/etc/mysql/conf.d：将主机当前目录下的 conf/my.cnf 挂载到容器的 /etc/mysql/my.cnf 
        -v $PWD/logs:/logs：将主机当前目录下的 logs 目录挂载到容器的 /logs
        -v $PWD/data:/var/lib/mysql ：将主机当前目录下的data目录挂载到容器的 /var/lib/mysql
        -e MYSQL_ROOT_PASSWORD=000000：初始化 root 用户的密码
    ```


- 拉取
    ```docker
        docker pull hub.c.163.com/library/mysql:latest 
    ```

- 运行
    ```docker
        docker run -p 3306:3306 -e MYSQL_ROOT_PASSWORD=000000 -d hub.c.163.com/library/mysql
        
        docker run -p 3306:3306 --name mysql -v $PWD/conf:/etc/mysql/conf.d -v $PWD/logs:/logs -v $PWD/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=000000 -d hub.c.163.com/library/mysql:5.6
    ```

### 常用docker-mysql(ubuntu 进入docker中操作mysql)命令 

- 查看当前运行的docker-mysql容器image或者启动时指定的name 并复制
    ```
    docker ps 
    ```
- 进入容器内, 当进入后看到 /# 或 /$ 代表已经进入
    ```
    docker exec -it mysql bash
    docker exec -it 823c967e60ca bash  
    ```
- 连接mysql, 当看到 mysql> 代表已经进入mysql
    ```
    mysql -uroot -p000000
    ```
- 退出
    - exit 退出mysql
    - 在执行exit 退出 docker-mysql 容器 
---


## Docker-redis

- 参考: 
    - https://www.cnblogs.com/lysongbo/p/9506782.html
    - 菜鸟教程: https://www.runoob.com/redis/redis-install.html
- 拉取
    ``` 
    docker pull hub.c.163.com/library/redis
    ```

- 运行
    ```
    docker run -d -p 6379:6379 --name redis hub.c.163.com/library/redis
    ```
