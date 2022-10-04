# 部署Trojan


<!--more-->

## 什么是Trojan
详细请自行Google或Baidu。

## 部署前提
1. 域名。必须使用域名，可以没有SSL证书。本文采用Namecheap注册的二级域名做demo。
2. 可连接上网的VPS。各种云服务商均可，本文以AWS的EC2做Demo。
   1. AWS提供一年免费的服务器，每个月750小时的访问。
   2. Azure提供USD200额度的免费账户。

## 部署流程
### 1. 创建EC2
省略截图
### 2. 连接EC2
省略截图
### 3. 安装。 （以下参照 https://github.com/Jrohy/trojan 大神做好的部署环境，可直接跳转参照）

```
[ec2-user@ip-172-31-30-131 ~]$ source <(curl -sL https://git.io/trojan-install)
正在安装trojan管理程序..
Error: You must be root to run this script
```
提示需要使用Root用户

### 4. 使用root
```
[ec2-user@ip-172-31-30-131 ~]$ sudo passwd root

Changing password for user root.
New password: 
Retype new password: 
passwd: all authentication tokens updated successfully.
```

### 5. 切换root
```
[ec2-user@ip-172-31-30-131 ~]$ su
Password: 
[root@ip-172-31-30-131 ec2-user]# 
```

### 6. 重新安装Trojan
```
#安装/更新
source <(curl -sL https://git.io/trojan-install)

#卸载
source <(curl -sL https://git.io/trojan-install) --remove

```

## Trojan客户端
### 移动版
推荐使用 Shadowrocket，真的是百搭，支持多种协议。IOS需要在，美国应用市场，现在3.5美金。
### 电脑版
可以使用TrojanX。
#### 下载推荐
除IOS外，可前往 https://dl.trojan-cdn.com/trojan/ 下载客户端。


