---
layout: post
title: "gem-stones"
date: 2014-07-11 14:38:44 +0800
comments: true
categories: Algorithm
tags: [Algorithm]

---

###[Gem-stones](https://www.hackerrank.com/challenges/gem-stones)

John has discovered various rocks. Each rock is composed of various elements, and each element is represented by a lowercase latin letter from 'a' to 'z'. An element can be present multiple times in a rock. An element is called a 'gem-element' if it occurs at least once in each of the rocks.

Given the list of rocks with their compositions, display the number of gem-elements that exist in those rocks.

<!--more-->

- Input Format 

The first line consists of N, the number of rocks. 
Each of the next N lines contain rocks' composition. Each composition consists of lowercase letters of English alphabet.

- Output Format 

Print the number gem-elements that exist in those rocks.

Constraints 
```
1 ≤ N ≤ 100 
Each composition consists of only small latin letters ('a'-'z'). 
1 ≤ Length of each composition ≤ 100
```
Sample Input

```
3
abcdde
baccd
eeabg
```
Sample Output

```
2
```
Explanation 
Only "a", "b" are the two kind of gem-elements, since these are the only characters that occur in each of the rocks' composition.

---
**The Code**:
    #include <iostream>
    #include <string.h>
    using namespace std;
    
    int main()
    {
        int N;
        int ele[26];
        char str[100];
        while(cin>>N)
        {
            int sum = 0;
            for(int i=0;i<26;i++)ele[i]=1;
            for(int i=0;i<N;i++)
            {
                cin>>str;
                int len = strlen(str);
                for(int j=0;j<len;j++)
                    if(ele[str[j]-'a']!=0)
                    ele[str[j]-'a']++;
                for(int k=0;k<26;k++)
                {        
                    if(ele[k]>1)
                        ele[k]=1;
                    else
                        ele[k]=0;
                } 
            } 
            for(int j=0;j<26;j++)
                    if(ele[j]==1)sum++;
                    
               printf("%d\n",sum);
            }
                
        return 0;    
    }

    ---

