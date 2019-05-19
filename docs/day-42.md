402.移掉k位数字

给定一个以字符串表示的非负整数 *num*，移除这个数中的 *k* 位数字，使得剩下的数字最小。

**注意:**

- *num* 的长度小于 10002 且 ≥ *k。*
- *num* 不会包含任何前导零。

**示例 1 :**

```
输入: num = "1432219", k = 3
输出: "1219"
解释: 移除掉三个数字 4, 3, 和 2 形成一个新的最小的数字 1219。
```

**示例 2 :**

```
输入: num = "10200", k = 1
输出: "200"
解释: 移掉首位的 1 剩下的数字为 200. 注意输出不能有任何前导零。
```

示例 **3 :**

```
输入: num = "10", k = 2
输出: "0"
解释: 从原数字移除所有的数字，剩余为空就是0。
```



##### 解题思路

观察几个例子我们能发现一个规律：

例子1中删除的是432；

例子2中删除的是1；

例子3中删除的是10；

它们都是降序序列，例子2看起来不明显，但是结合被删除的1后面的0一起看，也能发现它是降序序列。

那就简单了，我们用一个栈来记录每一位数；每次遍历到的数字都拿来和栈顶的数字进行对比，如果栈顶的数字比当前数字大，就把栈顶元素出栈（即移除这一位数），将当前元素入栈。这样处理后剩下的num序列应该是一个升序序列。

如果这个时候移除的数字还不够k个，那就继续出栈，直到够k个为止。因为升序序列，删除末尾的数字后得到的数列肯定会更小。

最后还得处理一下前导零。



##### 代码

```javascript
/**
 * @param {string} num
 * @param {number} k
 * @return {string}
 */
var removeKdigits = function(num, k) {
    let res=[];
    
    for(const number of num){
        while(res.length&&res[res.length-1]>number&&k){
            res.pop();
            k--;
        }
        res.push(number);
    }
    while(k){
        res.pop();
        k--;
    }
    while(res[0]==='0'){
        res.shift();
    }
    if(res.length===0)
        return '0';
    else
        return res.join('');
};
```



##### 总结

这一类题目得多列几种情况，看一下怎样才能使得剩下的数最小，这个处理过程中有没有什么步骤是有共同点的。把它们共同的特征提取出来就是算法了。



##### 封面
