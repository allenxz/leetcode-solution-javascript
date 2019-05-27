##### 406.根据身高重建队列

假设有打乱顺序的一群人站成一个队列。 每个人由一个整数对`(h, k)`表示，其中`h`是这个人的身高，`k`是排在这个人前面且身高大于或等于`h`的人数。 编写一个算法来重建这个队列。

**注意：**
总人数少于1100人。

**示例**

```
输入:
[[7,0], [4,4], [7,1], [5,0], [6,1], [5,2]]

输出:
[[5,0], [7,0], [5,2], [6,1], [4,4], [7,1]]
```



##### 解题思路

首先将people序列按身高从低到高排列，身高相同的按人数从大到小排列。

然后重建的时候，我们从最高的开始排，因为先排高的，身高低的入队的时候不会受人数限制；且身高相同的时候，应该先排人数小的。



##### 代码

```javascript
/**
 * @param {number[][]} people
 * @return {number[][]}
 */
var reconstructQueue = function(people) {
    people.sort(function (a,b){
        return a[0]===b[0]?b[1]-a[1]:a[0]-b[0];
    });
    let res=[];
    for(let i=people.length-1;i>=0;i--){
        res.splice(people[i][1],0,people[i]);
    }
    return res;
};
```



##### 总结

`res.splice(people[i][1],0,people[i])`可以完美的实现需求。

在当前序列的`people[i][1]`处插入`people[i]`，恰好满足人数的限制。