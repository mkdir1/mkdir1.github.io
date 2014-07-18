---
layout: post
title: "Insert interval"
date: 2014-07-18 15:40:02 +0800
comments: true
categories: algorithm
tags: leetcode

---
####leetcode-Insert interval
#####题干
Given a set of non-overlapping intervals, insert a new interval into the intervals (merge if necessary).

You may assume that the intervals were initially sorted according to their start times.

Example 1:
Given intervals [1,3],[6,9], insert and merge [2,5] in as [1,5],[6,9].

Example 2:
Given [1,2],[3,5],[6,7],[8,10],[12,16], insert and merge [4,9] in as [1,2],[3,10],[12,16].

This is because the new interval [4,9] overlaps with [3,5],[6,7],[8,10].

<!--more-->

这题被虐了十几次，耗时半日．

其实逻辑简单，只是处理起来麻烦，如果有调试会更简单，只是平台上面只有结果．

#####code

    /**
     * Definition for an interval.
     * struct Interval {
     *     int start;
     *     int end;
     *     Interval() : start(0), end(0) {}
     *     Interval(int s, int e) : start(s), end(e) {}
     * };
     */
    bool  cmp(Interval interval1, Interval interval2)
    {
            return interval1.start<interval2.start;
    }
    class Solution {
    public:
       
        vector<Interval> insert(vector<Interval> &intervals, Interval newInterval) 
        {
             int size = intervals.size();
             intervals.push_back(newInterval);
             if(size==0)
                return intervals;  // pitfall1
            sort(intervals.begin(), intervals.end(), cmp);
            vector<Interval> result;
            int starts, ends;
            size++;
            int i,j;
            for(i=0;i<size;i++)
            {
                starts = intervals[i].start;
                ends   = intervals[i].end;
                for(j=i+1;j<size;j++)
                {
                    if(ends<intervals[j].start)
                      {
                        Interval tmp(starts, ends);
                        result.push_back(tmp);
                         break;
                      }
                     else if(ends>=intervals[j].start&&ends<=intervals[j].end)
                     {
                         ends = intervals[j].end;
                         i = j; //pitfall2
                     }
                     else
                        i = j; //pitfall3
                }
                if(size==j)
                 {
                        Interval tmp(starts, ends);
                        result.push_back(tmp);
                        break;
                 }
            }
            return result;
        }
    };

三个pitfalls，首先按starts排序，然后遍历，其中要更新的不止是ends的值，还有是i也要更新，这样，就略过了．

#####Bug
- 1. 关于sort排序，应该放在class之外，否则会报错
- 2. vector也有sort函数


