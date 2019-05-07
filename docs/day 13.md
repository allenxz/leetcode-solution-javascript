> 快乐的颓废周末



##### 15. 三数之和

给定一个包含 *n* 个整数的数组 `nums`，判断 `nums` 中是否存在三个元素 *a，b，c ，*使得 *a + b + c =* 0 ？找出所有满足条件且不重复的三元组。

**注意：**答案中不可以包含重复的三元组。

```
例如, 给定数组 nums = [-1, 0, 1, 2, -1, -4]，

满足要求的三元组集合为：
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```



##### 解题思路

参考自：https://leetcode.com/problems/3sum/discuss/232712/Best-Python-Solution-(Explained)

首先我们对数组进行排序。这样子方便我们后面调节双指针。

我们在[0，nums.length-1]的范围内遍历nums数组中的每个数字，针对这每个数字，我们设置两个指针，左指针`l=i+1`，右指针`r=nums.length-1`。也就是在nums[i]后面的数字里找出两个数字使得`nums[i]+nums[l]+nums[r]`。

这个过程需要我们不断调节左右指针，如果三者总和大于0，说明r太大了，r--；如果三者之和小于0，说明l太小了，l++...直到三者之和恰好为0。

大概的思路就是这样，具体还有一些细节我写在注释里了。



##### 代码

```javascript
var threeSum = function(nums) {
    let res=[];
    nums.sort(function (a,b) {
        return a-b;
    });
		//遍历到nums.length-2
    //因为针对nums[i]需要找两个数，得空出两个位置。如果不够两个，直接return []
    for(let i=0;i<nums.length-2;i++){
      	//排序后第一个数都大于0，说明全员正数，无解
        if(nums[i]>0)
            break;
      	//跳过连续一样的数字，避免加入重复解
        if(i>0&&nums[i]===nums[i-1])
            continue;

        let l=i+1,r=nums.length-1;
        while (l<r) {
            let total=nums[i]+nums[l]+nums[r];
            if(total<0)
                l++;
            else if(total>0)
                r--;
            else{
                res.push([nums[i],nums[l],nums[r]]);
              	//跳过连续一样的数字，避免重复解
                while (l<r&&nums[l]===nums[l+1])
                    l++;
                while (l<r&&nums[r]===nums[r-1])
                    r--;
                l++;
                r--;
            }
        }
    }

    return res;
};
```



##### 总结

人家大神的思路说的很清楚了，也没什么好总结的。数组内找最优或者匹配问题的，一般都是双指针。可惜自己脑子蠢，没想出来。还有一个需要注意的是，javascript对纯数字数组的排序是可能会出错的，比如输入一个`[2,6,3,4,11,1]`，排序后是`[1, 11, 2, 3, 4, 6]`。

解决方法如下：

```javascript
arr.sort(function (a,b) {
    return a-b;
});
```

