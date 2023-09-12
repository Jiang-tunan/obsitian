### 1.合并两个有序数组
给你两个按 **非递减顺序** 排列的整数数组 `nums1` 和 `nums2`，另有两个整数 `m` 和 `n` ，分别表示 `nums1` 和 `nums2` 中的元素数目。请你 **合并** `nums2` 到 `nums1` 中，使合并后的数组同样按 **非递减顺序** 排列。
**注意：**最终，合并后数组不应由函数返回，而是存储在数组 `nums1` 中。为了应对这种情况，`nums1` 的初始长度为 `m + n`，其中前 `m` 个元素表示应合并的元素，后 `n` 个元素为 `0` ，应忽略。`nums2` 的长度为 `n` 。
**示例 1：**
**输入：**nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3
**输出：**[1,2,2,3,5,6]
**解释：**需要合并 [1,2,3] 和 [2,5,6] 。
合并结果是 [_**1**_,_**2**_,2,_**3**_,5,6] ，其中斜体加粗标注的为 nums1 中的元素。

**示例 2：**
**输入：**nums1 = [1], m = 1, nums2 = [], n = 0
**输出：**[1]
**解释：**需要合并 [1] 和 [] 。
合并结果是 [1] 。

**示例 3：**
**输入：**nums1 = [0], m = 0, nums2 = [1], n = 1
**输出：**[1]
**解释：**需要合并的数组是 [] 和 [1] 。
合并结果是 [1] 。
注意，因为 m = 0 ，所以 nums1 中没有元素。nums1 中仅存的 0 仅仅是为了确保合并结果可以顺利存放到 nums1 中。

**提示：**
- `nums1.length == m + n`
- `nums2.length == n`
- `0 <= m, n <= 200`
- `1 <= m + n <= 200`
- `-109 <= nums1[i], nums2[j] <= 109`

**进阶：**你可以设计实现一个时间复杂度为 `O(m + n)` 的算法解决此问题吗？
```c
void merge(int* nums1, int nums1Size, int m, int* nums2, int nums2Size, int n)  
{  
	int p1 = m - 1;  
	int p2 = n - 1;  
	int p = m + n - 1;  
  
	while (p1 >= 0 && p2 >= 0)  
	{  
		if (nums1[p1] < nums2[p2])  
		{  
			nums1[p] = nums2[p2];  
			p2--;  
		}  
		else  
		{  
			nums1[p] = nums1[p1];  
			p1--;  
		}  
		p--;  
	}  
	while (p2 >= 0)  
	{  
		nums1[p] = nums2[p2];  
		p2--;  
		p--;  
	}  
}
```
### 2.移除元素
给你一个数组 `nums` 和一个值 `val`，你需要 **[原地](https://baike.baidu.com/item/%E5%8E%9F%E5%9C%B0%E7%AE%97%E6%B3%95)** 移除所有数值等于 `val` 的元素，并返回移除后数组的新长度。
不要使用额外的数组空间，你必须仅使用 `O(1)` 额外空间并 **[原地](https://baike.baidu.com/item/%E5%8E%9F%E5%9C%B0%E7%AE%97%E6%B3%95) 修改输入数组**。元素的顺序可以改变。你不需要考虑数组中超出新长度后面的元素。

**说明:**
为什么返回数值是整数，但输出的答案是数组呢?
请注意，输入数组是以**「引用」**方式传递的，这意味着在函数里修改输入数组对于调用者是可见的。
你可以想象内部操作如下:
// **nums** 是以“引用”方式传递的。也就是说，不对实参作任何拷贝
`int len = removeElement(nums, val);`
// 在函数里修改输入数组对于调用者是可见的。
// 根据你的函数返回的长度, 它会打印出数组中 **该长度范围内** 的所有元素。
for (int i = 0; i < len; i++) {
    print(nums[i]);
}

**示例 1：**
**输入：**nums = [3,2,2,3], val = 3
**输出：**2, nums = [2,2]
**解释：**函数应该返回新的长度 **2**, 并且 nums 中的前两个元素均为 **2**。你不需要考虑数组中超出新长度后面的元素。例如，函数返回的新长度为 2 ，而 nums = [2,2,3,3] 或 nums = [2,2,0,0]，也会被视作正确答案。

**示例 2：**
**输入：**nums = [0,1,2,2,3,0,4,2], val = 2
**输出：**5, nums = [0,1,4,0,3]
**解释：**函数应该返回新的长度 **`5`**, 并且 nums 中的前五个元素为 **`0`**, **`1`**, **`3`**, **`0`**, **4**。注意这五个元素可为任意顺序。你不需要考虑数组中超出新长度后面的元素。

**提示：**
- `0 <= nums.length <= 100`
- `0 <= nums[i] <= 50`
- `0 <= val <= 100`
```c
int removeElement(int* nums, int numsSize, int val)  
{  
	if (numsSize == 0)  
	{  
		return 0;  
	}  
	int p = 0;  
	for (int i = 0; i < numsSize; i++)  
	{  
		if (nums[i] != val)  
		{  
			nums[p] = nums[i];  
			p++;  
		}  
	}  
	return p;  
}
```
### 3 删除有序数组中的重复项
给你一个 **升序排列** 的数组 `nums` ，请你 **[原地](http://baike.baidu.com/item/%E5%8E%9F%E5%9C%B0%E7%AE%97%E6%B3%95)** 删除重复出现的元素，使每个元素 **只出现一次** ，返回删除后数组的新长度。元素的 **相对顺序** 应该保持 **一致** 。然后返回 `nums` 中唯一元素的个数。

考虑 `nums` 的唯一元素的数量为 `k` ，你需要做以下事情确保你的题解可以被通过：
- 更改数组 `nums` ，使 `nums` 的前 `k` 个元素包含唯一元素，并按照它们最初在 `nums` 中出现的顺序排列。`nums` 的其余元素与 `nums` 的大小不重要。
- 返回 `k` 。

**判题标准:**
系统会用下面的代码来测试你的题解:
int[] nums = [...]; // 输入数组
int[] expectedNums = [...]; // 长度正确的期望答案
int k = removeDuplicates(nums); // 调用
assert k == expectedNums.length;
for (int i = 0; i < k; i++) {
    assert nums[i] == expectedNums[i];
}
如果所有断言都通过，那么您的题解将被 **通过**。

**示例 1：**
**输入：**nums = [1,1,2]
**输出：**2, nums = [1,2,_]
**解释：**函数应该返回新的长度 **`2`** ，并且原数组 _nums_ 的前两个元素被修改为 **`1`**, **`2`** `。`不需要考虑数组中超出新长度后面的元素。

**示例 2：**
**输入：**nums = [0,0,1,1,1,2,2,3,3,4]
**输出：**5, nums = [0,1,2,3,4]
**解释：**函数应该返回新的长度 **`5`** ， 并且原数组 _nums_ 的前五个元素被修改为 **`0`**, **`1`**, **`2`**, **`3`**, **`4`** 。不需要考虑数组中超出新长度后面的元素。

**提示：**
- `1 <= nums.length <= 3 * 104`
- `-104 <= nums[i] <= 104`
- `nums` 已按 **升序** 排列
```c
int removeDuplicates(int* nums, int numsSize)
{
    int i = 0;
    int j = 1;

    while(j < numsSize)
    {

        if (nums[i] != nums[j])
        {
            nums[i+1] = nums[j];
            i++;
            j++;
        }
        else
            j++;
    }
    return i+1;
}
```
### 4 删除多数元素
给定一个大小为 `n` 的数组 `nums` ，返回其中的多数元素。多数元素是指在数组中出现次数 **大于** `⌊ n/2 ⌋` 的元素。你可以假设数组是非空的，并且给定的数组总是存在多数元素。

**示例 1：**
**输入：**nums = [3,2,3]
**输出：**3

**示例 2：**
**输入：**nums = [2,2,1,1,1,2,2]
**输出：**2

**提示：**
- `n == nums.length`
- `1 <= n <= 5 * 104`
- `-109 <= nums[i] <= 109`
**进阶：**尝试设计时间复杂度为 O(n)、空间复杂度为 O(1) 的算法解决此问题
```c
int majorityElement(int* nums, int numsSize)
{
    int count = 1;
    int candidate = nums[0];

    for (int i = 1; i < numsSize; i++) 
    {
        if (count == 0)
         {
            candidate = nums[i];
        }
        count += (nums[i] == candidate) ? 1 : -1;
    }

    return candidate;
}
```
### 5 股票最佳时机
给定一个数组 `prices` ，它的第 `i` 个元素 `prices[i]` 表示一支给定股票第 `i` 天的价格。
你只能选择 **某一天** 买入这只股票，并选择在 **未来的某一个不同的日子** 卖出该股票。设计一个算法来计算你所能获取的最大利润。
返回你可以从这笔交易中获取的最大利润。如果你不能获取任何利润，返回 `0` 。
**示例 1：**
**输入：**[7,1,5,3,6,4]
**输出：**5
**解释：**在第 2 天（股票价格 = 1）的时候买入，在第 5 天（股票价格 = 6）的时候卖出，最大利润 = 6-1 = 5 。
     注意利润不能是 7-1 = 6, 因为卖出价格需要大于买入价格；同时，你不能在买入前卖出股票。

**示例 2：**
**输入：**prices = [7,6,4,3,1]
**输出：**0
**解释：**在这种情况下, 没有交易完成, 所以最大利润为 0。

**提示：**
- `1 <= prices.length <= 105`
- `0 <= prices[i] <= 104`
```c
`int maxProfit(int* prices, int pricesSize){
    if (pricesSize == 0) return 0;
    
    int minPrice = prices[0];
    int maxProfit = 0;
    for (int i = 1; i < pricesSize; i++) {

        if (prices[i] < minPrice) 
        {
		    minPrice = prices[i];
        } else if (prices[i] - minPrice > maxProfit) 
        {
            maxProfit = prices[i] - minPrice;
        }
    }
    return maxProfit;
}`
```
### 6 罗马数字转整数
罗马数字包含以下七种字符: `I`， `V`， `X`， `L`，`C`，`D` 和 `M`。

**字符**          **数值**
I             1
V             5
X             10
L             50
C             100
D             500
M             1000

例如， 罗马数字 `2` 写做 `II` ，即为两个并列的 1 。`12` 写做 `XII` ，即为 `X` + `II` 。 `27` 写做  `XXVII`, 即为 `XX` + `V` + `II` 。

通常情况下，罗马数字中小的数字在大的数字的右边。但也存在特例，例如 4 不写做 `IIII`，而是 `IV`。数字 1 在数字 5 的左边，所表示的数等于大数 5 减小数 1 得到的数值 4 。同样地，数字 9 表示为 `IX`。这个特殊的规则只适用于以下六种情况：

- `I` 可以放在 `V` (5) 和 `X` (10) 的左边，来表示 4 和 9。
- `X` 可以放在 `L` (50) 和 `C` (100) 的左边，来表示 40 和 90。 
- `C` 可以放在 `D` (500) 和 `M` (1000) 的左边，来表示 400 和 900。

给定一个罗马数字，将其转换成整数。

**示例 1:**
**输入:** s = "III"
**输出:** 3

**示例 2:**
**输入:** s = "IV"
**输出:** 4

**示例 3:**
**输入:** s = "IX"
**输出:** 9

**示例 4:**
**输入:** s = "LVIII"
**输出:** 58
**解释:** L = 50, V= 5, III = 3.

**示例 5:**
**输入:** s = "MCMXCIV"
**输出:** 1994
**解释:** M = 1000, CM = 900, XC = 90, IV = 4.

**提示：**
- `1 <= s.length <= 15`
- `s` 仅含字符 `('I', 'V', 'X', 'L', 'C', 'D', 'M')`
- 题目数据保证 `s` 是一个有效的罗马数字，且表示整数在范围 `[1, 3999]` 内
- 题目所给测试用例皆符合罗马数字书写规则，不会出现跨位等情况。
- IL 和 IM 这样的例子并不符合题目要求，49 应该写作 XLIX，999 应该写作 CMXCIX 。
- 关于罗马数字的详尽书写规则，可以参考 [罗马数字 - Mathematics](https://b2b.partcommunity.com/community/knowledge/zh_CN/detail/10753/%E7%BD%97%E9%A9%AC%E6%95%B0%E5%AD%97#knowledge_article) 。
```c
int romanToInt(char * s) {
    int len = strlen(s);
    int result = 0;

    for (int i = 0; i < len; i++) {
        switch (s[i]) {
            case 'I':
                if (i + 1 < len && (s[i + 1] == 'V' || s[i + 1] == 'X')) {
                    result -= 1;
                } else {
                    result += 1;
                }
                break;
            case 'V':
                result += 5;
                break;
            case 'X':
                if (i + 1 < len && (s[i + 1] == 'L' || s[i + 1] == 'C')) {
                    result -= 10;
                } else {
                    result += 10;
                }
                break;
            case 'L':
                result += 50;
                break;
            case 'C':
                if (i + 1 < len && (s[i + 1] == 'D' || s[i + 1] == 'M')) {
                    result -= 100;
                } else {
                    result += 100;
                }
                break;
            case 'D':
                result += 500;
                break;
            case 'M':
                result += 1000;
                break;
        }
    }

    return result;
}
// 时间复杂度是O(n)
```
### 7.最后一个单词的长度
给你一个字符串 `s`，由若干单词组成，单词前后用一些空格字符隔开。返回字符串中 **最后一个** 单词的长度。
**单词** 是指仅由字母组成、不包含任何空格字符的最大子字符串。

**示例 1：**
**输入：**s = "Hello World"
**输出：**5
**解释：**最后一个单词是“World”，长度为5。

**示例 2：**
**输入：**s = "   fly me   to   the moon  "
**输出：**4
**解释：**最后一个单词是“moon”，长度为4。

**示例 3：**
**输入：**s = "luffy is still joyboy"
**输出：**6
**解释：**最后一个单词是长度为6的“joyboy”。

**提示：**
- `1 <= s.length <= 104`
- `s` 仅有英文字母和空格 `' '` 组成
- `s` 中至少存在一个单词
```c
int lengthOfLastWord(char *s) {
    int len = strlen(s);
    int count = 0;

    // 从字符串末尾开始遍历
    for (int i = len - 1; i >= 0; i--) {
        // 如果遇到非空格字符，开始计数
        if (s[i] != ' ') {
            count++;
        }
        // 如果在计数期间遇到空格，停止计数并退出循环
        else if (count > 0) {
            break;
        }
    }
    return count;
}
```
### 8. 最长公共前缀
编写一个函数来查找字符串数组中的最长公共前缀。
如果不存在公共前缀，返回空字符串 `""`。

**示例 1：**
**输入：**strs = ["flower","flow","flight"]
**输出：**"fl"

**示例 2：**
**输入：**strs = ["dog","racecar","car"]
**输出：**""
**解释：**输入不存在公共前缀。

**提示：**
- `1 <= strs.length <= 200`
- `0 <= strs[i].length <= 200`
- `strs[i]` 仅由小写英文字母组成
```c
char* longestCommonPrefix(char** strs, int strsSize) {
    if (strsSize == 0) return "";
    static char res[1000];
    int index = 0;
    
    for (int i = 0; i < strlen(strs[0]); i++) {
        char c = strs[0][i];
        bool isCommon = true;

        for (int j = 1; j < strsSize; j++) {
            if (i >= strlen(strs[j]) || strs[j][i] != c) {
                isCommon = false;
                break;
            }
        }

        if (isCommon) {
            res[index++] = c;
        } else {
            break;
        }
    }
    res[index] = '\0';
    return res;
}
```
