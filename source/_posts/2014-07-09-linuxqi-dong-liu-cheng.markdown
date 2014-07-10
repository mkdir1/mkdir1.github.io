---
layout: post
title: "Linux启动流程"
date: 2014-07-09 23:14:18 +0800
comments: true
categories: Linux
tags: [linux,kernel]
keyword: linux

---

####Linux的启动顺序

- 1 加载BIOS的硬件信息并进行自检，然后根据设置取得第一个可启动的设备；

- 2 读取并执行第一个启动设备内MBR(master boot record,主引导分区)的boot loader；

- 3 依据bootloader的设置加载kernel，kernel开始检测硬件和加载驱动程序；

- 4 在硬件驱动成功后，kernel会调用init进程，init进程会取得run-level信息；

- 5 init执行/etc/rc.d/sysinit文件来准备软件执行的操作环境；

- 6 init执行run-level的各个服务；

- 7 init执行/etc/rc.d/rc.local文件；

- 8 init执行终端机模拟程序mingetty来启动login进程，最后等待用户登录。

---

####用户登录后

- 1 /etc/profile：此文件为系统的每个用户设置环境信息,当用户第一次登录时,该文件被执行. 并从/etc/profile.d目录的配置文件中搜集shell的设置。
    
- 2 /etc/bashrc: 为每一个运行bash shell的用户执行此文件.当bash shell被打开时,该文件被读取。

- 3 ~/.bash_profile: 每个用户都可使用该文件输入专用于自己使用的shell信息,当用户登录时,该文件仅仅执行一次!默认情况下,他设置一些环境变量,执行用户的.bashrc文件。

- 4 ~/.bashrc: 该文件包含专用于你的bash shell的bash信息,当登录时以及每次打开新的shell时,该该文件被读取。

- 5 ~/.bash_logout:当每次退出系统(退出bash shell)时,执行该文件.  另外,/etc/profile中设定的变量(全局)的可以作用于任何用户,而~/.bashrc等中设定的变量(局部)只能继承 /etc/profile中的变量,他们是"父子"关系。

- 6 ~/.bash_profile 是交互式、login 方式进入 bash 运行的~/.bashrc 是交互式 non-login 方式进入 bash 运行的通常二者设置大致相同，所以通常前者会调用后者。

---

