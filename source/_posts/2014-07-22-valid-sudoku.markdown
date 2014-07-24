---
layout: post
title: "valid-sudoku"
date: 2014-07-22 19:56:41 +0800
comments: true
categories: algorithm
tags: leetcode

---
####Valid Sudoku
The Sudoku board could be partially filled, where empty cells are filled with the character '.'.

A valid Sudoku board (partially filled) is not necessarily solvable. Only the filled cells need to be validated.

我这解法，绝对是对算法的侮辱～　哈哈

<!--more-->

Code:
    class Solution {
    public:
        bool isValidSudoku(vector<vector<char> > &board) 
        {
            for(int i=0;i<9;i++)
            for(int j=0;j<9;j++)
            {
                if(board[i][j]=='.')
                    continue;
                for(int k=j+1;k<9;k++)
                    if(board[i][j]==board[i][k])return false;
                for(int k=i+1;k<9;k++)
                    if(board[i][j]==board[k][j])return false;
                if(i%3==0&&j%3==0)
                {
                    if(board[i+1][j+1]!='.'&&board[i+1][j+1]==board[i][j])return false;
                    if(board[i+2][j+1]!='.'&&board[i+2][j+1]==board[i][j])return false;
                    if(board[i+1][j+2]!='.'&&board[i+1][j+2]==board[i][j])return false;
                    if(board[i+2][j+2]!='.'&&board[i+2][j+2]==board[i][j])return false;
                }
                if(i%3==0&&(j-1)%3==0)
                {
                    if(board[i+1][j-1]!='.'&&board[i+1][j-1]==board[i][j])return false;
                    if(board[i+2][j-1]!='.'&&board[i+2][j-1]==board[i][j])return false;
                    if(board[i+1][j+1]!='.'&&board[i+1][j+1]==board[i][j])return false;
                    if(board[i+2][j+1]!='.'&&board[i+2][j+1]==board[i][j])return false;   
                }
                if(i%3==0&&(j+1)%3==0)
                {
                    if(board[i+1][j-1]!='.'&&board[i+1][j-1]==board[i][j])return false;
                    if(board[i+2][j-1]!='.'&&board[i+2][j-1]==board[i][j])return false;
                    if(board[i+1][j-2]!='.'&&board[i+1][j-2]==board[i][j])return false;
                    if(board[i+2][j-2]!='.'&&board[i+2][j-2]==board[i][j])return false;   
                }
                if((i-1)%3==0&&j%3==0)
                {
                    if(board[i+1][j+1]!='.'&&board[i+1][j+1]==board[i][j])return false;
                    if(board[i+1][j+2]!='.'&&board[i+1][j+2]==board[i][j])return false;
                }
                if((i-1)%3==0&&(j-1)%3==0)
                {
                    if(board[i+1][j-1]!='.'&&board[i+1][j-1]==board[i][j])return false;
                    if(board[i+1][j+1]!='.'&&board[i+1][j+1]==board[i][j])return false;
                }
                 if((i-1)%3==0&&(j+1)%3==0)
                {
                    if(board[i+1][j-1]!='.'&&board[i+1][j-1]==board[i][j])return false;
                    if(board[i+1][j-2]!='.'&&board[i+1][j-2]==board[i][j])return false;
                }
                
            }
            return true;
        }
    };

好吧，管用就行，一遍过需要多仔细认真啊

这样代码还是很好看的，就是有点长

