---
title: Linux 常用命令
iscopyright: true
comments: true
lang: cn
tags:
  - linux
  - ubuntu
  - command
categories:
  - linux
abbrlink: linux
date: 2019-08-11 16:50:49
---


## 查看端口/进程
- 查看所有进程和端口使用情况
    - netstat –apn
- 用于查看某一端口的占用情况
    - lsof -i:端口号 
- 用于查看指定的端口号的进程情况
    - netstat -tunlp |grep 端口号
- 根据程序名称查询端口占用情况
    - ps -aux | grep 程序名称 #查看所有状态
    - ps -ef | grep 程序名称 #查看所有进程CMD进程信息
    - pgrep 程序名称 

- 杀死进程
    - kill -s 9 PID  #-s 9 制定了传递给进程的信号是9，即强制、尽快终止进程  
- 查看 xxx服务是否启动
    - systemctl status docker 查看状态
    - systemctl start docker 启动

## 其他命令
- 实时查看日志
    - tail -f 文件名称

- 查看系统日志 journalctl -xe


## 参考链接
- [Linux 最常用命令：解决 95% 以上的问题](https://mp.weixin.qq.com/s/FtLcT7PXlfwHKyTEKvnQxQ)
- [Linux下强制杀死进程的方法](https://www.cnblogs.com/liaojie970/p/7131043.html)
