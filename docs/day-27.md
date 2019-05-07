##### 33. 搜索旋转排序数组

假设按照升序排序的数组在预先未知的某个点上进行了旋转。

( 例如，数组 `[0,1,2,4,5,6,7]` 可能变为 `[4,5,6,7,0,1,2]` )。

搜索一个给定的目标值，如果数组中存在这个目标值，则返回它的索引，否则返回 `-1` 。

你可以假设数组中不存在重复的元素。

你的算法时间复杂度必须是 *O*(log *n*) 级别。

**示例 1:**

```
输入: nums = [4,5,6,7,0,1,2], target = 0
输出: 4
```

**示例 2:**

```
输入: nums = [4,5,6,7,0,1,2], target = 3
输出: -1
```



##### 解题思路

题目一开始就说了时间复杂度需要是O(nlogn)，这相当于明示了要用二分查找。知道了大概要用什么算法之后，我们对比一下，这道题和常规的二分查找区别在哪。

它是一个经过旋转过的升序数组，也就是说比nums[i]小的数不一定在i的左边，比nums[i]大的数也不一定在i的右边。这就在缩小查找范围时给我们带来点麻烦，换句话说，我们需要想一个方法，正确的判断target会落在哪个半区。

![](../images/搜索旋转排序数组.png)



##### 代码

```javascript
var search = function(nums, target) {
    let left=0,right=nums.length-1;
    while(left<=right){
        let middle=(left+right)/2|0;
        if(nums[middle]===target)
            return middle;
        else if(nums[middle]>target){
            if(nums[right]<nums[middle]&&target<=nums[right]){
                left=middle+1;
            }
            else{
                right=middle-1;
            }
        }
        else{
            if(nums[left]>nums[middle]&&target>=nums[left]){
                right=middle-1;
            }
            else{
                left=middle+1;
            }
        }
    }
    return -1;
};
```



##### 总结

这道题相当于是二分查找的变式，难度一般，关键在确定搜索的区间。根据旋转后的数组特征去判断target会落到的半区就行。

