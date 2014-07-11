---
layout: post
title: "Markdonw语法简要"
date: 2014-07-09 16:39:07 +0800
comments: true
categories: Language 
tags: [octopress, markdown]
keyword: octopress markdown

---

###Markdonw语法简要

此处权当工具参考之用，可覆盖90%应用

<!--more-->

---

#####标题和加粗斜体
- 用\#的个数表示标题大小
- 粗体和斜体用星号来括起来  

---

#####图片和链接
- 链接 
 \[linkname](url,"description")

- 图片   
 !\[name](url,"title")
    直接<img\>标签可以改变大小，这个可以尝试
    
- 两者都可以引用表示

---

#####引用
- 在行首加上<即可，可嵌套使用
- 引用内可支持其它的Markdown语法
- \用来转义

#####列表
- 使用\+/\-/\*俱可

#####代码块
- 代码块用一个tab或四个空格，块内的格式将保留，一直会持续到没有tab或文件完
- 可直接加入html标签，但前后要加空行
