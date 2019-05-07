> 下完棋写下算法，地精天下第一



##### 16. 最接近的三数之和

给定一个包括 *n* 个整数的数组 `nums` 和 一个目标值 `target`。找出 `nums` 中的三个整数，使得它们的和与 `target` 最接近。返回这三个数的和。假定每组输入只存在唯一答案。

```
例如，给定数组 nums = [-1，2，1，-4], 和 target = 1.

与 target 最接近的三个数的和为 2. (-1 + 2 + 1 = 2).
```



##### 解题思路

思路和昨天的几乎一模一样，我们还是先排序，然后遍历nums中前`nums.length-2`的每一个数，然后在其后面通过双指针找两个合适的数相加，指针还是左指针指向`i+1`，右指针指向`nums.length-1`，然后每次循环，先将三个数加起来，如果和比原来的值更接近target，覆盖原来的值，将其记录下来。如果和小于target，左指针右移；如果和小于target，右指针左移；如果恰好相等，直接返回target。



##### 代码

```javascript
var threeSumClosest = function(nums, target)  {
    let res=0;
    if(nums.length<3)
        return res;
    else
        res=nums[0]+nums[1]+nums[2];
    nums.sort(function (a,b) {
        return a-b;
    });

    for(let i=0;i<nums.length-2;i++){
        if(i>0&&nums[i]===nums[i-1])
            continue;

        let l=i+1,r=nums.length-1;
        while (l<r) {
            let total=nums[i]+nums[l]+nums[r];
            if(Math.abs(target-total)<Math.abs(res-target)){
                res=total;
            }
            if(total<target){
                l++;
            }
            else if(total>target){
                r--;
            }
            else{
                return target;
            }
        }
    }
    return res;
};
```



##### 总结

和昨天的思路类似，没什么好多说的。代码结构都基本是一样的。

不过最后还是有点话想说，算上今天，我已经连续写了两周了。一开始我怕自己坚持不了太久，但是慢慢的写下来，发下自己还是乐在其中。虽然每天都花一个多小时在算法上，短期的收益没见到多少，不过我很清楚，仅凭我现在的能力，进大厂无疑是痴人说梦，自己不是985出身，没发表过论文，ACM没拿过奖，我能依仗只有技术这条路。

所以我每天都在努力，让这个梦做得更长一点，更真实一点。直到有一天，万一瞎猫碰上死耗子，梦想成真了呢哈哈。