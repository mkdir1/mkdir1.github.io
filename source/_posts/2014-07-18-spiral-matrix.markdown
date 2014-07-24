---
layout: post
title: "Spiral Matrix"
date: 2014-07-18 19:01:52 +0800
comments: true
categories: algorithm
tags: leetcode

---
####[Spiral Matrix](https://oj.leetcode.com/problems/spiral-matrix/) 

#####Problem
Given a matrix of m x n elements (m rows, n columns), return all elements of the matrix in spiral order.

For example,

Given the following matrix:
```
    [1,2,3]
    [4,5,6]
    [7,8,9]
```
You should return`[1,2,3,6,8,9,7,4,5]`

<!--more-->

#####Code
```
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int> > &matrix)
    {
        vector<int>result;
        result.clear();
        int row = matrix.size();
        if(row==0)return result;
        int col = matrix[0].size();
        int rowleft = 0, rowright = col -1;
        int coltop = 0, colbott = row -1;
        int i=0,j=0;
        int dir = 1;
        while(rowleft<=rowright&&coltop<=colbott)
        {
            switch(dir)
            {
                case 1:   //toright
                    while(rowleft<=rowright&&j>=rowleft&&j<=rowright)
                    {
                        result.push_back(matrix[i][j]);
                        j++;
                    }
                    j--;
                    i++;
                    coltop++;
                    dir = 2;
                    break;
                case 2: //tobott
                   while(coltop<=colbott&&i>=coltop&&i<=colbott)
                   {
                       result.push_back(matrix[i][j]);
                       i++;
                   }
                   i--;
                   j--;
                   rowright--;
                   dir = 3;
                   break;
                case 3: //toleft
                 while(rowleft<=rowright&&j>=rowleft&&j<=rowright)
                 {
                     result.push_back(matrix[i][j]);
                     j--;
                 }
                 j++;
                 i--;
                 colbott--;
                 dir = 4;
                 break;
                case 4:  //totop
                 while(coltop<=colbott&&i>=coltop&&i<=colbott)
                 {
                      result.push_back(matrix[i][j]);
                      i--;
                 }
                 i++;
                 j++;
                 rowleft++;
                 dir = 1;
                 break;
                 default:
                    break;
            }
        }
      
        return result;
    }
};
```
有很多种方法，这是自己的一种实
