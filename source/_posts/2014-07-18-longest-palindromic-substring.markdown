---
layout: post
title: "Longest Palindromic Substring"
date: 2014-07-18 21:22:53 +0800
comments: true
categories: algorithm
tags: leetcode

---
#####[Longest Palindromic Substring](https://oj.leetcode.com/problems/longest-palindromic-substring/)
#####Probles

Given a string S, find the longest palindromic substring in S. You may assume that the maximum length of S is 1000, and there exists one unique longest palindromic substring.

看本站内的总结：[最长回文字符串](http://mkdir1.github.io/blog/2014/07/13/zui-xi-lie/)
<!--more-->
#####Code
```
class Solution {
public:
    string longestPalindrome(string s)
    {
        int len = s.length();
        string str="";
        if(len==0)return str;
        int maxlen = 0;
        int leng;
        int left,right;
        for(int i=0;i<2*len-1;i++)
        {
            if(i%2==0)
            {
                leng = 1;
                left = i/2 - 1;
                right = i/2 + 1;
                while(left>=0&&right<len&&s.at(left)==s.at(right))
                {
                    leng += 2;
                    left--;
                    right++;
                }
                 if(leng>maxlen)
              {
                    maxlen = leng;
                    str = s.substr(i/2-maxlen/2, maxlen);
              }
            }
            else
            {
                leng = 0;
                left = i/2;
                right = i/2+1;
                 while(left>=0&&right<len&&s[left]==s[right])
                {
                    leng += 2;
                    left--;
                    right++;
                }
               
            
             if(leng>maxlen)
              {
                    maxlen = leng;
                    str = s.substr(i/2-maxlen/2+1, maxlen);
              }
            }
        }
        return str;
    }
};
```
#####注意
- 1. 把奇偶统一起来，这样i的大小是2len-1的大小
- 2. 还有一个注意点是，substr()这个两个参数是指起始和长度，起始从0开始就算第一个
- 3. 后面两个if判断不能统一起来，因为substr中的参数不一样
- 4. 方法：**从中间向两边比较来判断是否回文，例a_b_c_b_a，则这个字符串abcba长度5，判断的位置有9个，然后从中间向两边展开，首先判断是否出界，再看是不是相等，这样最后更新长度和字符串**
- 5.　本文属于[最系列](http://mkdir1.github.io/blog/2014/07/13/zui-xi-lie/)的应用
