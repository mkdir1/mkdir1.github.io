---
layout: post
title: "rotate image"
date: 2014-07-18 16:44:12 +0800
comments: true
categories: algorithm
tags: leetcode

---

####[Rotate Image](https://oj.leetcode.com/problems/rotate-image/)
#####Problem:

You are given an n x n 2D matrix representing an image.

Rotate the image by 90 degrees (clockwise).

Follow up:
Could you do this in-place?

<!--more-->
#####Code:
    class Solution {
    public:
        void rotate(vector<vector<int> > &matrix)
        {
            int row = matrix.size();
            int col = matrix[0].size();
            // 
            for(int i=0;i<row;i++)
            for(int j=0;j<i;j++)
                swap(matrix[i][j],matrix[j][i]);
            //
            for(int i=0;i<row;i++)
            for(int j=0;j<col/2;j++)
                swap(matrix[i][j],matrix[i][col-1-j]);
                
        }
    };

#####说明
- 1.从windows下粘贴来的代码后面会有^M的结尾，原因是换行符的约定问题，在vim中很容易删除，用:%s/^M//g即可，但此处的^M需要用Ctrl+V再加上M得到

- 2.这题方法不是很多，先正对角线换，再左右换；或者逆对角线，再左右
