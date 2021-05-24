---
title: 剑指offer 04 数组查找
date: 2021-05-23
categories:
- 剑指offer
---
## 查找二维数组
- 题目
  - 在一个 n * m 的二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个高效的函数
    ，输入这样的一个二维数组和一个整数，判断数<组中是否含有该整数。限制：0 <= n <= 1000 ，0 <= m <= 1000

- 题解
  - 从上往下变小，从左往右变大，这个特性可以看出左下是最小，右上是最大。那就从左下开始循环，记为flag。
  - 如果flag > 目标数，则消去本行（因为左边是最小数，右边只会比最小的大，所以不在）
  - 如果flag<目标数，则消去列。目标数一定在他上面。
```java
class Solution {
    public boolean findNumberIn2DArray(int[][] matrix, int target) {
        int i = matrix.length-1, j=0;
        while(i>=0 && j <matrix[0].length){
            if(matrix[i][j] > target) i--; //消去行
            else if(matrix[i][j] < target) j++; //消去列
            else return true;
        }
        return false;
    }
}
```