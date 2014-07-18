---
layout: post
title: "C++中sort报错"
date: 2014-07-18 12:25:35 +0800
comments: true
categories: language

---
####C++中报错
** no matching function for call to 'sort'**
<!--more-->

具体：

代码如下：
    class Solution {
    public:
    bool  cmp(Interval interval1, Interval interval2)
    {
            return interval1.start<interval2.start;
    };
    int f()
    {
        ...
        sort(intervals.begin(),intervals.end(),cmp);
        ...
    }
    };
此处用法错误，不知是否察觉：

** no matching function for call to 'sort'**


解决之法：

将cmp的定义置于class之外

可以将sort定义在结构体之内，这样就直接intervals.sort(...)；如果定义在之外，要放在类的外面
