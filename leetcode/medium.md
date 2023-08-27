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