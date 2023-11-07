---
title: 'A dumb (but worked) solution to string matching problem'
date: 2023-11-06
permalink: /posts/DumbSM
tags:
  - String
  - Competitive Programming
---

When I attended Super Cup last year, I met [an interesting problem](https://oj.vnoi.info/problem/olp_sc22_bstr). I came up with a heuristic way to solve string matching problem and got AC. But until now, I still feel annoyed that I can't study about it more. I opened this blog post so that I can try to find something interesting.

&nbsp;  
You can repost, use, modify,... (do whatever you want to) this post, but if you do, please, write my name or the link to this blog as the source. This blog post is not final, I will update it when I can think of something worth putting.
  
&nbsp;  
Ok, here we begin.  

## Problem  
  
First of all, let me redefine the string matching problem:
> **String Matching Problem:**  Given two strings L and P. determine if P is a substring (a contiguous sequence of characters) of L.

&nbsp;  
Many algorithm like Hash, KMP, Z already solved this problem with the best possible time complexity (O(n + m), with n and m is the length of L and P, respectively).  
Here, my solution focus on the problems with update tasks (Can we do updates with KMP or Z? Honestly I don't know these algorithms much).
  
## Hypothesis 
My claim is kind of simple:  
> **Claim:**  Define U(R) as a set contain all K-substrings (substrings of length K) of a string R. If U(P) is subset of U(L), P is a substring of L. (K is a hyperparameter; In Super Cup, I choose K = 10).
  
&nbsp;  
Now, you may say, this would never work. Of course it won't work in worst cases, like when all character of P are the same. But will it work if all character of P and L are randomly generated?

## Probabilities

I'm bad at math. :<

## Expansion

### Generic query tasks

&nbsp;
Note that, two functions U and cnt described above are independent for each string. Suppose You have a fixed string L, in each query, you are given a string P (or updating a pre-defined P), and need to find F(L, P) (counting substrings, checking substring, insert/delete, etc...). F(L, P) can be found in O((len(P) * K * log(len(P) * K)) * (log(len(L)) * K)) as we only need to work on P (in most cases, we need to find all K-substrings in P and put them into a map, hence the complexity len(P) * K * log(len(P) * K)), and any interaction with L is through U or cnt, which take log(len(L)) * K each time (or log(len(L)) + K if we use hash).
  
### Substring counting 
  
> **Substring Counting Problem:**  Given two strings L and P. determine the number of times P appear in L as a substring.
  
&nbsp;
My solution to the problem: Define cnt(s,R) is the number of times a string s appear in a string R as a K-substring. The solution to the problem is the minimum cnt(s1, L) / cnt(s1, P) among all K-substring s1 of P.

### Insert/Delete Query

&nbsp;
To insert or delete a substring at a arbitrary position, just update K-substrings contain the character of those position. Insert/Delete in string can be done using a cartesian tree.
  
&nbsp;
To demonstrate how insert/delete work, I created this ugly-looking pic using MS Paint:  
![image](https://github.com/PTN407/PTN407.github.io/assets/92132592/20d95251-e8be-44ac-842b-04a5f11dec40)

### Longest common substring

&nbsp;
This can turn into "Find longest consecutive K-substring of P appear in L". Note that this only work if longest common substring have length of at least K, so if there are no consecutive K-substring of P appear in L, brute force all substring in P whose length < K.  
