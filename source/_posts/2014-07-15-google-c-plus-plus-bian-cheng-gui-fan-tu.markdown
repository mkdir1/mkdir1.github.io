---
layout: post
title: "google_c++编程规范图"
date: 2014-07-15 02:30:11 +0800
comments: true
categories: Language
tags: C++

---
##### Google C++ Style Guide
觅得神图一张，尽解Google C++ Style Guide

制作精美，详尽得当，不可多得

感谢原作者[voidccc](http://blog.csdn.net/voidccc/article/details/37599203)

<!--more-->

**原图（可另存）**

{% img /images/google_c++.png %}

#####总结一下
-  1. 文件名小写，可有下划线或短线，扩展为.cc
-  2. 开关加版权，许可证，作者，说明．．
-  3. .h文件顺序：本类的.h，C系统文件，C++系统文件，其它库，本项目头文件，避免用../.开关，要绝对路径指示.h
-  4. 禁止使用using namespace xx,而用using std::string

---
