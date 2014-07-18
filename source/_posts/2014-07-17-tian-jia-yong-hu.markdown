---
layout: post
title: "添加用户"
date: 2014-07-17 01:28:54 +0800
comments: true
categories: linux

---
####Linux下添加用户　
所涉及到的知识和概念比较多

<!--more-->
#####命令
**useradd**
    useradd [] name
    -b, --base-dir BASE_DIR	新账户的主目录的基目录
    -c, --comment COMMENT         新账户的 GECOS 字段
    -d, --home-dir HOME_DIR       新账户的主目录
    -D, --defaults		显示或更改默认的 useradd 配置
    -e, --expiredate EXPIRE_DATE  新账户的过期日期
    -f, --inactive INACTIVE       新账户的密码不活动期
    -g, --gid GROUP		新账户主组的名称或 ID
    -G, --groups GROUPS	新账户的附加组列表
    -h, --help                    显示此帮助信息并推出
    -k, --skel SKEL_DIR	使用此目录作为骨架目录
    -K, --key KEY=VALUE           不使用 /etc/login.defs 中的默认值
    -l, --no-log-init	不要将此用户添加到最近登录和登录失败数据库
    -m, --create-home	创建用户的主目录
    -M, --no-create-home		不创建用户的主目录
    -N, --no-user-group	不创建同名的组
    -o, --non-unique		允许使用重复的 UID 创建用户
    -p, --password PASSWORD		加密后的新账户密码
    -r, --system                  创建一个系统账户
    -R, --root CHROOT_DIR         chroot 到的目录
    -s, --shell SHELL		新账户的登录 shell
    -u, --uid UID			新账户的用户 ID
    -U, --user-group		创建与用户同名的组
    -Z, --selinux-user SEUSER		为 SELinux 用户映射使用指定 SEU
    sudo useradd -d /home/hadoop/ -g adm -s /bin/bash hadoop

- 1. 如果`-s /bin/sh`就会出现登录后只有一个$的情形，这是所选的shell出不对，应该换成/bin/bash
- 2. 所选的目录应该事先就创建一个 `-d`
- 3. -g 组名，可以查看`/etc/group`文件中的组名

**userdel**
    sudo userdel hadoop
**who,whoami,w,finger**
这此命令查看相关用户情况，是个很常用的命令，用法也很简单

#####概念
**组的分类**
- 1. 管理员 root:具有使用系统所有权限的用户,其UID 为0.
- 2. 普通用户: 即一般用户,其使用系统的权限受限,其UID为500-60000之间.
- 3. 系统用户 :保障系统运行的用户,一般不提供密码登录系统,其UID为1-499之间.

**文件**
- 1．/etc/passwd文件：
```
其格式：account：password：UID:GID:GECOS:diretory:shell
        account: 用户名或帐号
        password ：用户密码占位符
        UID：用户的ID号
        GID：用户所在组的ID号
        GECOS:用户的详细信息（如姓名，年龄，电话等）
        diretory：用户所的家目录
        shell：用户所在的编程环境
```              
- 2. /etc/shadow
```
   其格式：account：password：最近更改密码的日期：密码不可更该的天数：密码需要重新更改的天数：密码更改前的警告期限：密码过期的宽限时间：帐号失效日期：保留
```
**相关命令**
usermod, groupdd

