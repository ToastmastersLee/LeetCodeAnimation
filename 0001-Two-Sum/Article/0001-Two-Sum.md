# LeetCode 第 1 号问题：两数之和

> 本文首发于公众号「图解面试算法」，是 [图解 LeetCode ](<https://github.com/MisterBooo/LeetCodeAnimation>) 系列文章之一。
>
> 同步博客：https://www.algomooc.com
>

题目来源于 LeetCode 上第 1 号问题：两数之和。题目难度为 Easy，目前通过率为 45.8% 。

### 题目描述

给定一个整数数组 `nums` 和一个目标值 `target`，请你在该数组中找出和为目标值的那 **两个** 整数，并返回他们的数组下标。

你可以假设每种输入只会对应一个答案。但是，你不能重复利用这个数组中同样的元素。

**示例:**

```
给定 nums = [2, 7, 11, 15], target = 9

因为 nums[0] + nums[1] = 2 + 7 = 9
所以返回 [0, 1]
```

### 题目解析

使用查找表来解决该问题。

设置一个 map 容器 record 用来记录元素的值与索引，然后遍历数组 nums。

* 每次遍历时使用临时变量 complement 用来保存目标值与当前值的差值
* 在此次遍历中查找 record ，查看是否有与 complement 一致的值，如果查找成功则返回查找值的索引值与当前变量的值 i
* 如果未找到，则在 record 保存该元素与索引值 i

### 动画描述

![](../Animation/Animation.gif)

### 代码实现
#### C++
```
// 1. Two Sum
// https://leetcode.com/problems/two-sum/description/
// 时间复杂度：O(n)
// 空间复杂度：O(n)
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int,int> record;
        for(int i = 0 ; i < nums.size() ; i ++){
       
            int complement = target - nums[i];
            if(record.find(complement) != record.end()){
                int res[] = {i, record[complement]};
                return vector<int>(res, res + 2);
            }

            record[nums[i]] = i;
        }
        return {};
    }
};

```
#### C
```c
// 1. Two Sum
// https://leetcode.com/problems/two-sum/description/
// 时间复杂度：O(n)
// 空间复杂度：O(n)
/**
 * Note: The returned array must be malloced, assume caller calls free().
 */
int* twoSum(int* nums, int numsSize, int target, int* returnSize){
    int *ans=(int *)malloc(2 * sizeof(int));
    int i,j;
    bool flag=false; 
    for(i=0;i<numsSize-1;i++)
    {
        for(j=i+1;j<numsSize;j++)
        {
            if(nums[i]+nums[j] == target)
            {
                ans[0]=i;
                ans[1]=j;
                flag=true;
            }
        }
    }
    if(flag){
        *returnSize = 2;
    }
    else{
        *returnSize = 0;
    }
    return ans;
}
```
#### Java
```
// 1. Two Sum
// https://leetcode.com/problems/two-sum/description/
// 时间复杂度：O(n)
// 空间复杂度：O(n)
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int l = nums.length;
        int[] ans=new int[2];
        int i,j;
        for(i=0;i<l-1;i++)
        {
            for(j=i+1;j<l;j++)
            {
                if(nums[i]+nums[j] == target)
                {
                    ans[0]=i;
                    ans[1]=j;
                }
            }
        }
        
        return ans;
        
    }
}
```
#### Python
```
# 1. Two Sum
# https://leetcode.com/problems/two-sum/description/
# 时间复杂度：O(n)
# 空间复杂度：O(n)
class Solution(object):
    def twoSum(self, nums, target):
        l = len(nums)
        print(nums)
        ans=[]
        for i in range(l-1):
            for j in range(i+1,l):
                if nums[i]+nums[j] == target:
                    ans.append(i)
                    ans.append(j)
                    print([i,j])
                    break
        return ans
```



#### C#

```c#
public class Solution {
    public int[] TwoSum(int[] nums, int target) {
        // 创建哈希表，用于存储已遍历过的数字及其索引
        Dictionary<int, int> hashtable = new Dictionary<int, int>();

        // 遍历数组
        for (int i = 0; i < nums.Length; i++) {
            // 计算当前数字与目标值的差值
            int complement = target - nums[i];

            // 在哈希表中查找是否存在与当前数字匹配的差值
            if (hashtable.ContainsKey(complement)) {
                // 如果存在，则返回两个数字的索引
                return new int[] { hashtable[complement], i };
            }

            // 如果哈希表中不包含当前数字，将当前数字及其索引添加到哈希表中
            if (!hashtable.ContainsKey(nums[i])) {
                hashtable.Add(nums[i], i);
            }
        }

        // 如果未找到匹配的两个数字，返回空数组
        return new int[0];
    }
}
```



| 改动前                                                       | 改动后                                                       |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| <img src="./img/image-20240115174940043.png" alt="image-20240115174940043" style="zoom:50%;" /> | <img src="./img/image-20240115175010856.png" alt="image-20240115175010856" style="zoom: 50%;" /> |



##### 面试脚本

https://chat.openai.com/c/71aadd95-8269-4652-bcc7-699867198a83

### 1. Overall Approach:

**Goal:** Find two numbers in the array that add up to the given target.

**Approach:**

- Utilize a hash table to efficiently store and look up values.
- Iterate through the array, and for each element, check if its complement (target minus the current element) is in the hash table.

### 2. Step-by-Step Explanation:

#### Step 1:

**Initialization:**

- Initialize an empty hash table to store encountered elements.

#### Step 2:

**Iterate Through the Array:**

- For each element in the array:
  - Calculate the complement (target minus the current element).
  - Check if the complement exists in the hash table.

#### Step 3:

**Check Complement:**

- If the complement is found in the hash table:
  - Return the indices of the current element and its complement.

#### Step 4:

**Update Hash Table:**

- If the complement is not found:
  - Add the current element and its index to the hash table.

#### Step 5:

**Completion:**

- If the loop completes without finding a match:
  - Return an empty array to indicate no solution.

### 3. English Explanation:

Let's start with initializing an empty hash table. As we iterate through the array, for each element, we calculate its complement, which is the target minus the current element. We then check if this complement exists in the hash table. If it does, we've found our pair, and we return the indices. If not, we add the current element and its index to the hash table for future reference. If the loop completes without finding a match, we return an empty array, signaling that no solution exists.

This approach ensures an efficient runtime by leveraging the constant-time lookup capability of a hash table. The key is to keep track of encountered elements and their indices to quickly identify pairs. Please feel free to ask if you need clarification on any specific step!



![](../../Pictures/qrcode.jpg)
