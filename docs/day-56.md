##### 365. 水壶问题

有两个容量分别为 *x*升 和 *y*升 的水壶以及无限多的水。请判断能否通过使用这两个水壶，从而可以得到恰好 *z*升 的水？

如果可以，最后请用以上水壶中的一或两个来盛放取得的 *z升* 水。

你允许：

- 装满任意一个水壶
- 清空任意一个水壶
- 从一个水壶向另外一个水壶倒水，直到装满或者倒空

**示例 1:** (From the famous [*"Die Hard"* example](https://www.youtube.com/watch?v=BVtQNK_ZUJg))

```
输入: x = 3, y = 5, z = 4
输出: True
```

**示例 2:**

```
输入: x = 2, y = 6, z = 5
输出: False
```



##### 解题思路

也没有故意去找，但是今天还是挑了一道数学题来做。

题目的意思转化一下其实等价于：

**是否存在整数a，b使得ax+by=z**，我们假设下x，y的最小公约数为d，那么ax+by即等价于nd(n为大于或等于1的整数)，所以问题就变成了是否存在整数n，使得**nd=z**，即x，y的最小公约数能否被z整除。



##### 代码

```javascript
/**
 * @param {number} x
 * @param {number} y
 * @param {number} z
 * @return {boolean}
 */
var canMeasureWater = function(x, y, z) {
    if(x+y<z)
        return false;
    if(x===z||y==z)
        return true;
    let d=gcd(x,y);
    return z%d===0?true:false;
    
    function gcd(x,y){
        if(y===0)
            return x;
        return gcd(y,x%y);
    }
};
```



##### 总结

本来是想跳过这道数学题的，不过因为比较简单。想赶紧A了以后看比赛写博客去了，所以就水了一把嘻嘻。以后应该不刷这类的数学题了，或者说不用数学方式来解了。因为面试应该还是考虑算法思维多一点。



