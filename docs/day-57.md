##### 228. 汇总区间

给定一个无重复元素的有序整数数组，返回数组区间范围的汇总。

**示例 1:**

```
输入: [0,1,2,4,5,7]
输出: ["0->2","4->5","7"]
解释: 0,1,2 可组成一个连续的区间; 4,5 可组成一个连续的区间。
```

**示例 2:**

```
输入: [0,2,3,4,6,8,9]
输出: ["0","2->4","6","8->9"]
解释: 2,3,4 可组成一个连续的区间; 8,9 可组成一个连续的区间。
```



##### 解题思路

题意和思路都挺容易。感觉像是Easy的题目。

不过我写的比较原始，用个flag来记录当前的状态，是连续还是非连续。然后在连续状态的终点把连续的区间写进res中。这里得注意连续区间是否只是一个点，得特殊处理。



##### 代码

```javascript
/**
 * @param {number[]} nums
 * @return {string[]}
 */
var summaryRanges = function(nums) {
    if(nums.length===1)
        return [nums[0]+''];
    let res=[];
    let flag=0,start,end;
    for(let i=0;i<nums.length;i++){
        if(flag===0){
            start=nums[i];
            end=nums[i];
            flag=1;
        }
        else{
            if(nums[i]===end+1){
                end++;
                if(i===nums.length-1){
                    res.push(start+'->'+end);
                }
            }
            else{
                if(start===end){
                    res.push(start+'');
                }
                else{
                    res.push(start+'->'+end);
                }
                start=end=nums[i];
                if(i===nums.length-1){
                    res.push(start+'');
                    return res;
                }
                flag=1;
            }
        }
    }
    return res;
};
```

