---
title: "在AWS的EC2上部署Trojan"
date: 2022-02-06T16:00:06+08:00
draft: true
description: 一键部署Trojan
---

<!--more-->

## 什么是Trojan
详细请自行Google或Baidu。

## 部署

### 前提
1. 域名。必须使用域名，可以没有SSL证书。本文采用Namecheap注册的二级域名做demo。
2. 可连接上网的VPS。各种云服务商均可，本文以AWS的EC2做Demo。AWS提供一年免费的服务器，每个月750小时的访问。

### 部署流程
1. 创建EC2
2. 连接EC2
3. 安装。 参照https://github.com/Jrohy/trojan 大神做好的部署环境

```
[ec2-user@ip-172-31-30-131 ~]$ source <(curl -sL https://git.io/trojan-install)
正在安装trojan管理程序..
Error: You must be root to run this script
```
提示需要使用Root用户

4. 使用root
```
[ec2-user@ip-172-31-30-131 ~]$ sudo passwd root

Changing password for user root.
New password: 
Retype new password: 
passwd: all authentication tokens updated successfully.
```

5. 切换root
```
[ec2-user@ip-172-31-30-131 ~]$ su
Password: 
[root@ip-172-31-30-131 ec2-user]# 
```

6. 重新安装Trojan
```
#安装/更新
source <(curl -sL https://git.io/trojan-install)

#卸载
source <(curl -sL https://git.io/trojan-install) --remove

```

7. 

## 