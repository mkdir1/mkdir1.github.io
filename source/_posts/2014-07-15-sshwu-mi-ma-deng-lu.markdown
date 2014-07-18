---
layout: post
title: "ssh无密码登录"
date: 2014-07-15 00:30:04 +0800
comments: true
categories: Linux
tags: ssh

---
####ssh无密码登录

<!--more-->

ssh应用太广，最常用的就是远程登录和文件传输了，每次输入密码和登录确实很浪费时间，这里就不需要输入密码了

#####设置

-  1. 在客户端．生成密钥`ssh-keygen -t rsa`，这样在~/.ssh文件夹中就会有一个公钥和一个私钥
-  2. 服务端，在~/.ssh中，将客户端的id_rsa.phb放到这里，`scp .ssh/id_rsa.phb ip:.ssh/authorizend_keys`，也可以命名其它的
-  3. 再登录时就可以不用输入密码．也可以把登录alias写入bash中，scp时也不用输入密码，但是还是要记住ip

