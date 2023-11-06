---
title: 'A dumb (but worked) solution to string matching problem'
date: 2023-11-06
permalink: /posts/DumbSM
tags:
  - String
  - Competitive Programming
---

When I attended Super Cup last year, I met [an interesting problem](https://oj.vnoi.info/problem/olp_sc22_bstr). I came up with a heuristic way to solve string matching problem and got AC. But until now, I still feel annoyed that I can't study about it more. I opened this blog post so that I can try to find something interesting.

You can repost, use, modify,... (do whatever you want) this post, but if you do, please, write my name or the link to this blog as the source. This blog post is not final, I will update it when I can think of something worth putting.

Ok, here we begin.  

First of all, let I redefine the string matching problem:

> **String Matching Problem:**  Given two strings L and P. determine if P is a substring (a contiguous sequence of characters) of L.

Many algorithm like Hash, KMP, Z already solved this problem with the best possible time complexity (O(n + m), with n and m is the length of L and P, respectively). Here, my solution 

