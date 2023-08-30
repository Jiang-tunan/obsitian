### 1 删除有序数组中的重复项
给你一个有序数组 `nums` ，请你 **[原地](http://baike.baidu.com/item/%E5%8E%9F%E5%9C%B0%E7%AE%97%E6%B3%95)** 删除重复出现的元素，使得出现次数超过两次的元素**只出现两次** ，返回删除后数组的新长度。不要使用额外的数组空间，你必须在 **[原地](https://baike.baidu.com/item/%E5%8E%9F%E5%9C%B0%E7%AE%97%E6%B3%95) 修改输入数组** 并在使用 O(1) 额外空间的条件下完成。

你可以想象内部操作如下:
// **nums** 是以“引用”方式传递的。也就是说，不对实参做任何拷贝
int len = removeDuplicates(nums);
// 在函数里修改输入数组对于调用者是可见的。
// 根据你的函数返回的长度, 它会打印出数组中 **该长度范围内** 的所有元素。
for (int i = 0; i < len; i++) {
    print(nums[i]);
}

**示例 1：**
**输入：**nums = [1,1,1,2,2,3]
**输出：**5, nums = [1,1,2,2,3]
**解释：**函数应返回新长度 length = **`5`**, 并且原数组的前五个元素被修改为 **`1, 1, 2, 2,`** **3** 。 不需要考虑数组中超出新长度后面的元素。

**示例 2：**
**输入：**nums = [0,0,1,1,1,1,2,3,3]
**输出：**7, nums = [0,0,1,1,2,3,3]
**解释：**函数应返回新长度 length = **`7`**, 并且原数组的前五个元素被修改为 **`0`**, **0**, **1**, **1**, **2**, **3**, **3 。** 不需要考虑数组中超出新长度后面的元素。

**提示：**
- `1 <= nums.length <= 3 * 104`
- `-104 <= nums[i] <= 104`
- `nums` 已按升序排列
```c
int removeDuplicates(int* nums, int numsSize) {
    if (numsSize <= 2)
	{
        return numsSize;
    }
    int insertPos = 2; // 由于可以保留两个重复的元素，所以从第三个位置开始检查

    for (int i = 2; i < numsSize; i++)
     {
        if (nums[i] != nums[insertPos - 2]) 
        {
            nums[insertPos] = nums[i];
            insertPos++;
        }
    }
    return insertPos;
```
### 2. 轮转数组
给定一个整数数组 `nums`，将数组中的元素向右轮转 `k` 个位置，其中 `k` 是非负数。

**示例 1:**
**输入:** nums = [1,2,3,4,5,6,7], k = 3
**输出:** `[5,6,7,1,2,3,4]`
**解释:**
向右轮转 1 步: `[7,1,2,3,4,5,6]`
向右轮转 2 步: `[6,7,1,2,3,4,5]`
向右轮转 3 步: `[5,6,7,1,2,3,4]`

**示例 2:**
**输入：**nums = [-1,-100,3,99], k = 2
**输出：**[3,99,-1,-100]
**解释:** 
向右轮转 1 步: [99,-1,-100,3]
向右轮转 2 步: [3,99,-1,-100]

**提示：**
- `1 <= nums.length <= 105`
- `-231 <= nums[i] <= 231 - 1`
- `0 <= k <= 105`

**进阶：**
- 尽可能想出更多的解决方案，至少有 **三种** 不同的方法可以解决这个问题。
- 你可以使用空间复杂度为 `O(1)` 的 **原地** 算法解决这个问题吗？
```c
void rotate(int* nums, int numsSize, int k) {
    k %= numsSize;  // 如果k大于numsSize，取模以避免多余的旋转
    reverse(nums, 0, numsSize - 1);
    reverse(nums, 0, k - 1);
    reverse(nums, k, numsSize - 1);``
}

void reverse(int* nums, int start, int end) {
    while (start < end) {
        int temp = nums[start];
        nums[start] = nums[end];
        nums[end] = temp;
        start++;
        end--;
    }
}
```
### 3 买卖股票的最佳时机
给你一个整数数组 `prices` ，其中 `prices[i]` 表示某支股票第 `i` 天的价格。
在每一天，你可以决定是否购买和/或出售股票。你在任何时候 **最多** 只能持有 **一股** 股票。你也可以先购买，然后在 **同一天** 出售。返回 _你能获得的 **最大** 利润_ 。

**示例 1：**
**输入：**prices = [7,1,5,3,6,4]
**输出：**7
**解释：**在第 2 天（股票价格 = 1）的时候买入，在第 3 天（股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5 - 1 = 4 。
     随后，在第 4 天（股票价格 = 3）的时候买入，在第 5 天（股票价格 = 6）的时候卖出, 这笔交易所能获得利润 = 6 - 3 = 3 。
     总利润为 4 + 3 = 7 。

**示例 2：**
**输入：**prices = [1,2,3,4,5]
**输出：**4
**解释：**在第 1 天（股票价格 = 1）的时候买入，在第 5 天 （股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5 - 1 = 4 。
     总利润为 4 。

**示例 3：**
**输入：**prices = [7,6,4,3,1]
**输出：**0
**解释：**在这种情况下, 交易无法获得正利润，所以不参与交易可以获得最大利润，最大利润为 0 。

**提示：**
- `1 <= prices.length <= 3 * 104`
- `0 <= prices[i] <= 104`

```c
int maxProfit(int* prices, int pricesSize) {

    int profit = 0;

    for (int i = 1; i < pricesSize; i++) {

        if (prices[i] > prices[i - 1]) {

            profit += prices[i] - prices[i - 1];

        }

    }

    return profit;

}
```
### 4 跳远游戏
给你一个非负整数数组 `nums` ，你最初位于数组的 **第一个下标** 。数组中的每个元素代表你在该位置可以跳跃的最大长度。
判断你是否能够到达最后一个下标，如果可以，返回 `true` ；否则，返回 `false` 。

**示例 1：**
**输入：**nums = [2,3,1,1,4]
**输出：**true
**解释：**可以先跳 1 步，从下标 0 到达下标 1, 然后再从下标 1 跳 3 步到达最后一个下标。

**示例 2：**
**输入：**nums = [3,2,1,0,4]
**输出：**false
**解释：**无论怎样，总会到达下标为 3 的位置。但该下标的最大跳跃长度是 0 ， 所以永远不可能到达最后一个下标。

**提示：**
- `1 <= nums.length <= 104`
- `0 <= nums[i] <= 105`
```c
bool canJump(int* nums, int numsSize){
  int maxReach = 0;
  for (int i = 0; i < numsSize; i++) {
    if (i <= maxReach) {
      maxReach = fmax(maxReach, i + nums[i]);
      if (maxReach >= numsSize - 1) {
        return true;
      }
	}
  }
  return false;
}
```
### 5. 跳跃游戏2
给定一个长度为 `n` 的 **0 索引**整数数组 `nums`。初始位置为 `nums[0]`。每个元素 `nums[i]` 表示从索引 `i` 向前跳转的最大长度。换句话说，如果你在 `nums[i]` 处，你可以跳转到任意 `nums[i + j]` 处:
- `0 <= j <= nums[i]` 
- `i + j < n`
返回到达 `nums[n - 1]` 的最小跳跃次数。生成的测试用例可以到达 `nums[n - 1]`。

**示例 1:**
**输入:** nums = [2,3,1,1,4]
**输出:** 2
**解释:** 跳到最后一个位置的最小跳跃数是 `2`。
     从下标为 0 跳到下标为 1 的位置，跳 `1` 步，然后跳 `3` 步到达数组的最后一个位置。

**示例 2:**
**输入:** nums = [2,3,0,1,4]
**输出:** 2

**提示:**
- `1 <= nums.length <= 104`
- `0 <= nums[i] <= 1000`
- 题目保证可以到达 `nums[n-1]`
```c
int jump(int* nums, int numsSize) {
    if (numsSize <= 1) return 0;
    int current_max = 0;  // 当前能够到达的最远位置
    int next_max = 0;     // 下一步能够到达的最远位置
    int jumps = 0;        // 跳跃的次数

    for (int i = 0; i < numsSize - 1; i++) {
        next_max = (i + nums[i] > next_max) ? i + nums[i] : next_max;
        if (i == current_max) {
            jumps++;
            current_max = next_max;
        }
    }  
    return jumps;
}
```