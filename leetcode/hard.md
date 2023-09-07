# 1. 加油站
在一条环路上有 `n` 个加油站，其中第 `i` 个加油站有汽油 `gas[i]` 升。
你有一辆油箱容量无限的的汽车，从第 `i` 个加油站开往第 `i+1` 个加油站需要消耗汽油 `cost[i]` 升。你从其中的一个加油站出发，开始时油箱为空。
给定两个整数数组 `gas` 和 `cost` ，如果你可以按顺序绕环路行驶一周，则返回出发时加油站的编号，否则返回 `-1` 。如果存在解，则 **保证** 它是 **唯一** 的。

**示例 1:**
**输入:** gas = [1,2,3,4,5], cost = [3,4,5,1,2]
**输出:** 3
**解释:**
从 3 号加油站(索引为 3 处)出发，可获得 4 升汽油。此时油箱有 = 0 + 4 = 4 升汽油
开往 4 号加油站，此时油箱有 4 - 1 + 5 = 8 升汽油
开往 0 号加油站，此时油箱有 8 - 2 + 1 = 7 升汽油
开往 1 号加油站，此时油箱有 7 - 3 + 2 = 6 升汽油
开往 2 号加油站，此时油箱有 6 - 4 + 3 = 5 升汽油
开往 3 号加油站，你需要消耗 5 升汽油，正好足够你返回到 3 号加油站。
因此，3 可为起始索引。

**示例 2:**
**输入:** gas = [2,3,4], cost = [3,4,3]
**输出:** -1
**解释:**
你不能从 0 号或 1 号加油站出发，因为没有足够的汽油可以让你行驶到下一个加油站。
我们从 2 号加油站出发，可以获得 4 升汽油。 此时油箱有 = 0 + 4 = 4 升汽油
开往 0 号加油站，此时油箱有 4 - 3 + 2 = 3 升汽油
开往 1 号加油站，此时油箱有 3 - 3 + 3 = 3 升汽油
你无法返回 2 号加油站，因为返程需要消耗 4 升汽油，但是你的油箱只有 3 升汽油。
因此，无论怎样，你都不可能绕环路行驶一周。

**提示:**
- `gas.length == n`
- `cost.length == n`
- `1 <= n <= 105`
- `0 <= gas[i], cost[i] <= 104`1.
```c
int canCompleteCircuit(int* gas, int gasSize, int* cost, int costSize) {
    int totalGas = 0;
    int totalCost = 0;
    int tank = 0;
    int start = 0;

    for (int i = 0; i < gasSize; i++) {
        totalGas += gas[i];
        totalCost += cost[i];
        tank += gas[i] - cost[i];
        if (tank < 0) {
            start = i + 1;
            tank = 0;
        }
    }

    if (totalGas < totalCost) {
        return -1;
    } else {
        return start;
    }
}
```
# 2. 分糖果
`n` 个孩子站成一排。给你一个整数数组 `ratings` 表示每个孩子的评分。
你需要按照以下要求，给这些孩子分发糖果：
- 每个孩子至少分配到 `1` 个糖果。
- 相邻两个孩子评分更高的孩子会获得更多的糖果。
请你给每个孩子分发糖果，计算并返回需要准备的 **最少糖果数目** 。

**示例 1：**
**输入：**ratings = [1,0,2]
**输出：**5
**解释：**你可以分别给第一个、第二个、第三个孩子分发 2、1、2 颗糖果。

**示例 2：**
**输入：**ratings = [1,2,2]
**输出：**4
**解释：**你可以分别给第一个、第二个、第三个孩子分发 1、2、1 颗糖果。
     第三个孩子只得到 1 颗糖果，这满足题面中的两个条件。

**提示：**
- `n == ratings.length`
- `1 <= n <= 2 * 104`
- `0 <= ratings[i] <= 2 * 104`
```c
int candy(int* ratings, int ratingsSize) {
    int* candies = (int*)malloc(sizeof(int) * ratingsSize);
    for (int i = 0; i < ratingsSize; i++) {
        candies[i] = 1;
    }

    // 从左到右遍历
    for (int i = 1; i < ratingsSize; i++) {
        if (ratings[i] > ratings[i - 1]) {
            candies[i] = candies[i - 1] + 1;
        }
    }

    // 从右到左遍历
    for (int i = ratingsSize - 2; i >= 0; i--) {
        if (ratings[i] > ratings[i + 1] && candies[i] <= candies[i + 1]) {
            candies[i] = candies[i + 1] + 1;
        }
    }

    int totalCandies = 0;
    for (int i = 0; i < ratingsSize; i++) {
        totalCandies += candies[i];
    }

    free(candies);
    return totalCandies;
}
// 时间复杂度o(n)
```
# 3 接雨水
给定 `n` 个非负整数表示每个宽度为 `1` 的柱子的高度图，计算按此排列的柱子，下雨之后能接多少雨水。

**示例 1：**
![](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/10/22/rainwatertrap.png)
**输入：**height = [0,1,0,2,1,0,1,3,2,1,2,1]
**输出：**6
**解释：**上面是由数组 [0,1,0,2,1,0,1,3,2,1,2,1] 表示的高度图，在这种情况下，可以接 6 个单位的雨水（蓝色部分表示雨水）。 

**示例 2：**
**输入：**height = [4,2,0,3,2,5]
**输出：**9

**提示：**
- `n == height.length`
- `1 <= n <= 2 * 104`
- `0 <= height[i] <= 105`
```c
int trap(int* height, int heightSize) {
    if (heightSize == 0) return 0;

    int* leftMax = (int*)malloc(sizeof(int) * heightSize);
    int* rightMax = (int*)malloc(sizeof(int) * heightSize);

    leftMax[0] = height[0];
    for (int i = 1; i < heightSize; i++) {
        leftMax[i] = (height[i] > leftMax[i - 1]) ? height[i] : leftMax[i - 1];
    }

    rightMax[heightSize - 1] = height[heightSize - 1];
    for (int i = heightSize - 2; i >= 0; i--) {
        rightMax[i] = (height[i] > rightMax[i + 1]) ? height[i] : rightMax[i + 1];
    }

    int totalWater = 0;
    for (int i = 0; i < heightSize; i++) {
        totalWater += (leftMax[i] < rightMax[i] ? leftMax[i] : rightMax[i]) - height[i];
    }

    free(leftMax);
    free(rightMax);
    return totalWater;
}
// 时间复杂度是O(n)
```