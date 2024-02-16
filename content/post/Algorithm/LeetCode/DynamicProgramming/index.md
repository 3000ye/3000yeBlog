---
title: Dynamic Programming
description: LeetCode Dynamic Programming
date: 2024-01-10T22:12:43+08:00
image: assets/leetcode.png
math: true
toc: true
categories:
    - Algorithm
tags:
    - LeetCode
    - Dynamic Programming
---

# [Dynamic Programming](https://leetcode.com/problemset/?topicSlugs=dynamic-programming&page=1)

## [Easy Dynamic Programming](https://leetcode.com/problemset/?topicSlugs=dynamic-programming&page=1&difficulty=EASY)

### [Climbing Stairs](https://leetcode.com/problems/climbing-stairs/description/)

```cpp
#include <bits/stdc++.h>
#include <vector>
using namespace std;

/*
 * @lc app=leetcode id=70 lang=cpp
 *
 * [70] Climbing Stairs
 */

// @lc code=start
class Solution {
public:
    int climbStairs(int n) {
        vector<int> ls = {1, 1};

        while (n > ls.size() - 1) {
            int x = ls[ls.size() - 1];
            int y = ls[ls.size() - 2];
            ls.push_back(x + y);
        }

        return ls[n];
    }
};
// @lc code=end
```


<!-- 
## [Medium Dynamic Programming](https://leetcode.com/problemset/?topicSlugs=dynamic-programming&page=1&difficulty=MEDIUM)

### [Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/description/) -->
