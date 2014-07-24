---
layout: post
title: "leetcode-combination sum"
date: 2014-07-22 17:05:12 +0800
comments: true
categories: algorithm
tags: leetcode
---
####Combination Sum 
Given a set of candidate numbers (C) and a target number (T), find all unique combinations in C where the candidate numbers sums to T.

The same repeated number may be chosen from C unlimited number of times.

Note:

All numbers (including target) will be positive integers.
Elements in a combination (a1, a2, … , ak) must be in non-descending order. (ie, a1 ≤ a2 ≤ … ≤ ak).

The solution set must not contain duplicate combinations.
For example, given candidate set 2,3,6,7 and target 7, 
A solution set is: 
```
[2,3,6,7] 7
[7] 
[2, 2, 3] 

```
<!--more-->
这题真是基础，之前一直对此类不知所措，现在略通一二，甚喜

Code:
    class Solution {
    public:
        void Getcom(vector<int>&can, int target, vector<vector<int>>&result, int level, int &sumcurrent, int nsize, vector<int>&tmp)
        {
            if(sumcurrent>target)return;
            if(target==sumcurrent)
            {
                result.push_back(tmp);
                return;
            }
            for(int i=level;i<nsize;i++)
            {
               
                    sumcurrent += can[i];
                    tmp.push_back(can[i]);
                    Getcom(can,target,result,i,sumcurrent,nsize,tmp);
                    tmp.pop_back();
                    sumcurrent -=can[i];
            }
            
        }
        vector<vector<int> > combinationSum(vector<int> &candidates, int target) 
        {
           vector<vector<int>> result;
           vector<int>tmp;
           int size = candidates.size();
           sort(candidates.begin(),candidates.end());
           int sumc = 0;
           Getcom(candidates,target,result,0,sumc,size,tmp);
           return result;
        }
    };

DFS方便记录结果，DP方便记数
