---
title: LeetCode-Day6
date: 2018-08-16 12:00:00
tags:
---

### 旋转图像 	LeetCode-48

##### 题目

给定一个 *n* × *n* 的二维矩阵表示一个图像。

将图像顺时针旋转 90 度。

**说明：**

你必须在**原地**旋转图像，这意味着你需要直接修改输入的二维矩阵。**请不要**使用另一个矩阵来旋转图像。

**示例 1:**

```
给定 matrix = 
[
  [1,2,3],
  [4,5,6],
  [7,8,9]
],

原地旋转输入矩阵，使其变为:
[
  [7,4,1],
  [8,5,2],
  [9,6,3]
]
```

**示例 2:**

```
给定 matrix =
[
  [ 5, 1, 9,11],
  [ 2, 4, 8,10],
  [13, 3, 6, 7],
  [15,14,12,16]
], 

原地旋转输入矩阵，使其变为:
[
  [15,13, 2, 5],
  [14, 3, 4, 1],
  [12, 6, 8, 9],
  [16, 7,10,11]
]
```

##### 思路

这个题很简单，规律和思路直接看代码吧

```c++
class Solution {
public:
    void rotate(vector<vector<int>>& matrix) {
        int a = matrix[0].size();
        int temp[a][a] = {0};
        for (int i = 0; i < a; i++) {
            for (int j = 0; j < a; j++) {
                temp[i][j] = matrix[a-j-1][i];
            }
        }
        for (int i = 0; i < a; i++) {
            for (int j = 0; j < a; j++) {
                matrix[i][j] = temp[i][j];
            }
        }
    }
};
```

但是这样实际是违背了题意= =，题上明确说了要**原地，不能使用另一个矩阵来旋转**

所以我们重新写一个，先把左下部分和右上部分交换，再左右镜像一下，任务完成。

```
[1,2,3]
[4,5,6]
[7,8,9]
//先把左下部分和右上部分交换
[1,4,7]
[2,5,8]
[3,6,9]
//左右镜像
[7,4,1]
[8,5,2]
[9,6,3]
```

```c++
class Solution {
public:
    void rotate(vector<vector<int>>& matrix) {
        int a = matrix[0].size();
        for (int i = 0; i < a; i++) {
            for (int j = i; j < a; j++) {
                std::swap(matrix[i][j],matrix[j][i]);
            }
        }
        for (int i = 0; i < a; i++) {
            for (int j = 0; j < a/2; j++) {
                std::swap(matrix[i][j],matrix[i][a-j-1]);
            }
        }
    }
};
```

