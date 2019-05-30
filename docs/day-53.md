##### 75. 颜色分类

给定一个包含红色、白色和蓝色，一共 *n* 个元素的数组，**原地**对它们进行排序，使得相同颜色的元素相邻，并按照红色、白色、蓝色顺序排列。

此题中，我们使用整数 0、 1 和 2 分别表示红色、白色和蓝色。

**注意:**
不能使用代码库中的排序函数来解决这道题。

**示例:**

```
输入: [2,0,2,1,1,0]
输出: [0,0,1,1,2,2]
```

**进阶：**

- 一个直观的解决方案是使用计数排序的两趟扫描算法。
  首先，迭代计算出0、1 和 2 元素的个数，然后按照0、1、2的排序，重写当前数组。
- 你能想出一个仅使用常数空间的一趟扫描算法吗？



##### 解题思路

要是单纯的完成这道题的话，难度很低，随便用一种排序都行。

不过要是原地，且是单遍扫描的话，就得要用到一个比较经典的算法---三路快排。

简单直白地说，就是我们遍历数组，遇到0，就放到数组的头部，遇到2，就放到数组的尾部；

排好0和2之后，1自然也就是有序的了。



##### 代码

```javascript
/**
 * @param {number[]} nums
 * @return {void} Do not return anything, modify nums in-place instead.
 */
var sortColors = function(nums) {
    if(nums.length>1){
        let left=-1,right=nums.length,cur=0;
        while(cur<right){
            if(nums[cur]<1){
                left++;
                [nums[cur],nums[left]]=[nums[left],nums[cur]];
                cur++;
            }
            else if(nums[cur]>1){
                right--;
                [nums[cur],nums[right]]=[nums[right],nums[cur]];
            }
            else
                cur++;
        }
    }
    return nums;
};
```
