---
layout: post
title: "unique binary search trees ii"
date: 2014-07-18 16:14:31 +0800
comments: true
categories: algorithm
tags: leetcode

---
####[Unique Binary Search Tree II](https://oj.leetcode.com/problems/unique-binary-search-trees-ii/)

<!--more-->

#####Problem
Given n, generate all structurally unique BST's (binary search trees) that store values 1...n.


#####Code

    /**
     * Definition for binary tree
     * struct TreeNode {
     *     int val;
     *     TreeNode *left;
     *     TreeNode *right;
     *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
     * };
     */
    class Solution {
    public:
        vector<TreeNode *> generate(int beg, int end)
        {
            vector<TreeNode* > ret;
            if (beg > end)
            {
                ret.push_back(NULL);
                return ret;
            }
            
            for(int i = beg; i <= end; i++)
            {
                vector<TreeNode* > leftTree = generate(beg, i - 1);
                vector<TreeNode* > rightTree = generate(i + 1, end);
                for(int j = 0; j < leftTree.size(); j++)
                    for(int k = 0; k < rightTree.size(); k++)
                    {
                        TreeNode *node = new TreeNode(i + 1);
                        ret.push_back(node);
                        node->left = leftTree[j];
                        node->right = rightTree[k];              
                    }           
            }
            
            return ret;
        }
        
        vector<TreeNode *> generateTrees(int n) {
            return generate(0, n - 1);
        }
    };

#####注意
- 1.此题第一想法就应试是递归或DFS

