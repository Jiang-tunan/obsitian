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
### 6 整数转罗马数字
罗马数字包含以下七种字符： `I`， `V`， `X`， `L`，`C`，`D` 和 `M`。

**字符**          **数值**
I             1
V             5
X             10
L             50
C             100
D             500
M             1000

例如， 罗马数字 2 写做 `II` ，即为两个并列的 1。12 写做 `XII` ，即为 `X` + `II` 。 27 写做  `XXVII`, 即为 `XX` + `V` + `II` 。

通常情况下，罗马数字中小的数字在大的数字的右边。但也存在特例，例如 4 不写做 `IIII`，而是 `IV`。数字 1 在数字 5 的左边，所表示的数等于大数 5 减小数 1 得到的数值 4 。同样地，数字 9 表示为 `IX`。这个特殊的规则只适用于以下六种情况：

- `I` 可以放在 `V` (5) 和 `X` (10) 的左边，来表示 4 和 9。
- `X` 可以放在 `L` (50) 和 `C` (100) 的左边，来表示 40 和 90。 
- `C` 可以放在 `D` (500) 和 `M` (1000) 的左边，来表示 400 和 900。

给你一个整数，将其转为罗马数字。

**示例 1:**
**输入:** num = 3
**输出:** "III"

**示例 2:**
**输入:** num = 4
**输出:** "IV"

**示例 3:**
**输入:** num = 9
**输出:** "IX"

**示例 4:**
**输入:** num = 58
**输出:** "LVIII"
**解释:** L = 50, V = 5, III = 3.

**示例 5:**
**输入:** num = 1994
**输出:** "MCMXCIV"
**解释:** M = 1000, CM = 900, XC = 90, IV = 4.

**提示：**
- `1 <= num <= 3999`
```c
char* intToRoman(int num) {
    // 定义罗马数字和对应的值
    char* symbols[] = {"M", "CM", "D", "CD", "C", "XC", "L", "XL", "X", "IX", "V", "IV", "I"};
    int values[] = {1000, 900, 500, 400, 100, 90, 50, 40, 10, 9, 5, 4, 1};

    // 为结果分配空间
    char* result = (char*)malloc(20 * sizeof(char));
    memset(result, 0, 20 * sizeof(char));

    int index = 0;
    for (int i = 0; i < 13; i++) {
        while (num >= values[i]) {
            strcat(result, symbols[i]);
            num -= values[i];
        }
    }

    return result;
}
// 时间复杂度是O(1)

```
### 7. 
实现`RandomizedSet` 类：
- `RandomizedSet()` 初始化 `RandomizedSet` 对象
- `bool insert(int val)` 当元素 `val` 不存在时，向集合中插入该项，并返回 `true` ；否则，返回 `false` 。
- `bool remove(int val)` 当元素 `val` 存在时，从集合中移除该项，并返回 `true` ；否则，返回 `false` 。
- `int getRandom()` 随机返回现有集合中的一项（测试用例保证调用此方法时集合中至少存在一个元素）。每个元素应该有 **相同的概率** 被返回。

你必须实现类的所有函数，并满足每个函数的 **平均** 时间复杂度为 `O(1)` 。

**示例：**
**输入**
["RandomizedSet", "insert", "remove", "insert", "getRandom", "remove", "insert", "getRandom"]
[[], [1], [2], [2], [], [1], [2], []]
**输出**
[null, true, false, true, 2, true, false, 2]

**解释**
RandomizedSet randomizedSet = new RandomizedSet();
randomizedSet.insert(1); // 向集合中插入 1 。返回 true 表示 1 被成功地插入。
randomizedSet.remove(2); // 返回 false ，表示集合中不存在 2 。
randomizedSet.insert(2); // 向集合中插入 2 。返回 true 。集合现在包含 [1,2] 。
randomizedSet.getRandom(); // getRandom 应随机返回 1 或 2 。
randomizedSet.remove(1); // 从集合中移除 1 ，返回 true 。集合现在包含 [2] 。
randomizedSet.insert(2); // 2 已在集合中，所以返回 false 。
randomizedSet.getRandom(); // 由于 2 是集合中唯一的数字，getRandom 总是返回 2 。

**提示：**
- `-231 <= val <= 231 - 1`
- 最多调用 `insert`、`remove` 和 `getRandom` 函数 `2 *` `105` 次
- 在调用 `getRandom` 方法时，数据结构中 **至少存在一个** 元素。
```c

```
### 8. N 字形变换
将一个给定字符串 `s` 根据给定的行数 `numRows` ，以从上往下、从左到右进行 Z 字形排列。
比如输入字符串为 `"PAYPALISHIRING"` 行数为 `3` 时，排列如下：

P   A   H   N
A P L S I I G
Y   I   R

之后，你的输出需要从左往右逐行读取，产生出一个新的字符串，比如：`"PAHNAPLSIIGYIR"`。
请你实现这个将字符串进行指定行数变换的函数：string convert(string s, int numRows);

**示例 1：**
**输入：**s = "PAYPALISHIRING", numRows = 3
**输出：**"PAHNAPLSIIGYIR"

**示例 2：**
**输入：**s = "PAYPALISHIRING", numRows = 4
**输出：**"PINALSIGYAHRPI"
**解释：**
P     I    N
A   L S  I G
Y A   H R
P     I

**示例 3：**
**输入：**s = "A", numRows = 1
**输出：**"A"

**提示：**
- `1 <= s.length <= 1000`
- `s` 由英文字母（小写和大写）、`','` 和 `'.'` 组成
- `1 <= numRows <= 1000`
```C
char* convert(char* s, int numRows) {
    if (numRows == 1) return s;

    int len = strlen(s);
    char* result = (char*)malloc(len + 1);
    int idx = 0;

    char** rows = (char**)malloc(numRows * sizeof(char*));
    for (int i = 0; i < numRows; i++) {
        rows[i] = (char*)malloc(len + 1);
        rows[i][0] = '\0';
    }

    int curRow = 0;
    int direction = -1; // -1: 向上, 1: 向下

    for (int i = 0; i < len; i++) {
        int rowLen = strlen(rows[curRow]);
        rows[curRow][rowLen] = s[i];
        rows[curRow][rowLen + 1] = '\0';

        if (curRow == 0 || curRow == numRows - 1) {
            direction = -direction;
        }
        curRow += direction;
    }

    for (int i = 0; i < numRows; i++) {
        int rowLen = strlen(rows[i]);
        for (int j = 0; j < rowLen; j++) {
            result[idx++] = rows[i][j];
        }
        free(rows[i]);
    }
    free(rows);

    result[idx] = '\0';
    return result;
}
// 时间复杂度是O(n)，空间复杂度也是O(n)
### 8.反转字符串中单词
给你一个字符串 `s` ，请你反转字符串中 **单词** 的顺序。
**单词** 是由非空格字符组成的字符串。`s` 中使用至少一个空格将字符串中的 **单词** 分隔开。
返回 **单词** 顺序颠倒且 **单词** 之间用单个空格连接的结果字符串。

**注意：**输入字符串 `s`中可能会存在前导空格、尾随空格或者单词间的多个空格。返回的结果字符串中，单词间应当仅用单个空格分隔，且不包含任何额外的空格。

**示例 1：**
**输入：**s = "`the sky is blue`"
**输出：**"`blue is sky the`"

**示例 2：**
**输入：**s = "  hello world  "
**输出：**"world hello"
**解释：**反转后的字符串中不能存在前导空格和尾随空格。

**示例 3：**
**输入：**s = "a good   example"
**输出：**"example good a"
**解释：**如果两个单词间有多余的空格，反转后的字符串需要将单词间的空格减少到仅有一个。

**提示：**
- `1 <= s.length <= 104`
- `s` 包含英文大小写字母、数字和空格 `' '`
- `s` 中 **至少存在一个** 单词

**进阶：**如果字符串在你使用的编程语言中是一种可变数据类型，请尝试使用 `O(1)` 额外空间复杂度的 **原地** 解法。
```c
void reverse(char* s, int start, int end) {
    while (start < end) {
        char temp = s[start];
        s[start] = s[end];
        s[end] = temp;
        start++;
        end--;
    }
}

char* reverseWords(char* s) {
    int n = strlen(s);
    // 反转整个字符串
    reverse(s, 0, n - 1);
    int start = 0, end = 0, idx = 0;
    while (start < n) {
        while (start < n && s[start] == ' ') start++; // 跳过前导空格
        if (start == n) break; // 如果已经到字符串末尾，退出循环
        if (idx != 0) s[idx++] = ' '; // 添加单词之间的空格
        end = start;
        while (end < n && s[end] != ' ') end++; // 找到单词的结束位置
        // 反转单个单词
        reverse(s, start, end - 1);
        // 复制单词到正确的位置
        for (int i = start; i < end; i++) {
            s[idx++] = s[i];
        }
        start = end;
    }
    s[idx] = '\0'; // 添加字符串结束符
    return s;
}
```