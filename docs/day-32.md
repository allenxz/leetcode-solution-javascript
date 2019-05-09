##### 41. 缺失的第一个正数

给定一个未排序的整数数组，找出其中没有出现的最小的正整数。

**示例 1:**

```
输入: [1,2,0]
输出: 3
```

**示例 2:**

```
输入: [3,4,-1,1]
输出: 2
```

**示例 3:**

```
输入: [7,8,9,11,12]
输出: 1
```

**说明:**

你的算法的时间复杂度应为O(*n*)，并且只能使用常数级别的空间。



##### 解题思路

这是一道Hard难度的题，是真的没思路，然后就果断上Discuss膜拜大佬了。

人家大佬果然是大佬。大佬的思路是这样的，第一次遍历数组，把nums[i]≥1且nums[i]≤nums.length的数放在他们“该在”的位置。这一步是算法的核心，举个例子，nums[i]=2，就把它和数组中的第2个数交换，即nums[nums[i]-1]；按照这样操作后，整个数组就会变成--->如果原本数组有这个数，那么它就会等于自己的下标加一。即第二个数是2，第三个数是3。

然而nums[i]≥1是为了排除非正整数，我们不需要考虑它们；nums[i]≤nums.length是为了排除那些太大的数，因为解的最大值为nums.length+1，那些太大的数我们也不需要考虑。

时间复杂度为O(2n)=O(n)，完美解决，再次膜拜。



##### 代码

```javascript
var firstMissingPositive = function(nums) {
    for(let i=0;i<nums.length;i++){
        if(nums[i]!=i+1){
            while(nums[i]>0&&nums[i]<=nums.length&&nums[nums[i-1]!=nums[i]]){
                let tmp=nums[i];
                nums[i]=nums[nums[i]-1];
                nums[tmp-1]=tmp;
            }
        }
    }
    for(let i=0;i<nums.length;i++){
        if(nums[i]!=i+1)
            return i+1;
    }
    return nums.length+1;
};
```



##### 总结

其实回头看官方给的提示也挺命中要点的，但是怪自己太蠢没get到。

* Think about how you would solve the problem in non-constant space. Can you apply that logic to the existing space?

  想想加入没有空间限制，我们会怎么做这道题，能不能将相同的逻辑应用到现有空间？这提示我们给在原地给数组"排序"。

* We don't care about duplicates or non-positive integers

  我们不需要考虑那些重复的和非正整数。提示我们“排序”的范围

* Remember that O(2n) = O(n)

  O(2n) = O(n)，时间复杂度上是相等的。提示我们扫描两遍数组。

