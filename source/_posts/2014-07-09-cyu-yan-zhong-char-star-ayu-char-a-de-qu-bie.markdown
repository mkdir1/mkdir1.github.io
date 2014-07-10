---
layout: post
title: "C语言中char *a与char a[]的区别"
date: 2014-07-09 23:41:57 +0800
comments: true
categories: C

---

#### C语言char s[] 和 char *s的区别

看如下的代码，区别立现

    char *s = "hello world";
    char s[] = "hello world"

区别在于**前者是指针，后者是数组**

    char *s是一个指向只读区域的指针，只读区域是hello world
    char s[]是一个数组，内容是拷贝了只读区别的数据

前者指针指向的内容不能变，后者可变

---
