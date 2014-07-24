---
layout: post
title: "sudoku-solver"
date: 2014-07-22 20:27:47 +0800
comments: true
categories: algorithm
tags: leetcode

---
####Sudoku Solver

Write a program to solve a Sudoku puzzle by filling the empty cells.

Empty cells are indicated by the character '.'.

You may assume that there will be only one unique solution.
<!--more-->
递归的方法，确实不错～　
#####Code

    bool isValid(vector<vector<char> > &board, int a, int b) {
    		int i,j;
    		for(i = 0; i < 9; i++)
    			if(i != a && board[i][b] == board[a][b])
    				return false;
    
    		for(j = 0; j < 9; j++)
    			if(j != b && board[a][j] == board[a][b])
    				return false;
    
    		int x = a/3*3;
    		int y = b/3*3;
    		for(i = 0; i < 3; i++)
    			for(j = 0; j< 3; j++)
    				if(x+i != a && y+j != b && board[x+i][y+j] == board[a][b])
    					return false;
    		return true;
        }
    	bool solveSudokudfs(vector<vector<char> > &board)
    	{
    		for(int i = 0; i < 9; i++)
    			for(int j = 0; j < 9; j++)
    			{
    				if(board[i][j] == '.')
    				{
    					for(int k = 1; k <= 9; k++)
    					{
    						board[i][j] = '0' + k;
    						if(isValid(board,i,j) && solveSudokudfs(board))
    							return true;
    						board[i][j] = '.';
    					}
    					return false;
    				}
    			}
    		return true;
    	}
    	void solveSudoku(vector<vector<char> > &board) {
            // Note: The Solution object is instantiated only once.
            solveSudokudfs(board);
        }

