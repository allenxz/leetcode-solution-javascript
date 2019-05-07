> 有些人表面在写算法，其实脑子里全是复联



##### 16. 四数之和

给定一个包含 *n* 个整数的数组 `nums` 和一个目标值 `target`，判断 `nums` 中是否存在四个元素 *a，**b，c* 和 *d* ，使得 *a* + *b* + *c* + *d* 的值与 `target` 相等？找出所有满足条件且不重复的四元组。

**注意：**

答案中不可以包含重复的四元组。

**示例：**

```
给定数组 nums = [1, 0, -1, 0, -2, 2]，和 target = 0。

满足要求的四元组集合为：
[
  [-1,  0, 0, 1],
  [-2, -1, 1, 2],
  [-2,  0, 0, 2]
]
```



##### 解题思路

又是n数和，和之前的题目一样，核心是双指针的搜索，但是不同的是，这个题目还混杂着分治的思想，把4数之和转换成3数之和，然后再把3数之和转成2数之和，然后进行双指针搜索就好。



##### 代码

```javascript
var fourSum = function(nums, target) {
    let res=[];
    if(nums.length<4)
        return res;
    nums.sort(function (a,b) {
        return a-b;
    });
    for(let i=0;i<nums.length;i++){
        if(i>0&&nums[i]===nums[i-1])
            continue;
        //4数之和转成3数之和
        let target1=target-nums[i];
        for(let j=i+1;j<nums.length;j++){
            if(j>i+1&&nums[j]===nums[j-1])
                continue;
            //3数之和转成2数之和
            let target2=target1-nums[j];
            let l=j+1,r=nums.length-1;
            while (l<r){
                let total=nums[l]+nums[r];
                if(total<target2)
                    l++;
                else if(total>target2)
                    r--;
                else {
                    res.push([nums[i],nums[j],nums[l],nums[r]]);
                    //去重
                    while(l<r&&nums[l]===nums[l+1])
                        l++;
                    while(l<r&&nums[r]===nums[r-1])
                        r--;
                    l++;
                    r--;
                }
            }
        }
    }
    return res;
};
```



##### 总结

首先把题目的复杂度降低，即将4数和转换成2数和，然后再设置双指针，去寻找两个合适的数。做多了思路其实都一样，可以参照前面第13天和第14天的题目，互相对应，理解会更深。