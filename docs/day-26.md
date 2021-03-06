##### 32.  最长有效括号

给定一个只包含 `'('` 和 `')'` 的字符串，找出最长的包含有效括号的子串的长度。

**示例 1:**

```
输入: "(()"
输出: 2
解释: 最长有效括号子串为 "()"
```

**示例 2:**

```
输入: ")()())"
输出: 4
解释: 最长有效括号子串为 "()()"
```



##### 解题思路

这道题我弄完之后看了下导论区，有用dp解的，也有用很巧妙的方法，正反扫描两遍去解。

我这用的栈，每次匹配到合法的括号时就计算当前连续的合法括号长度。

栈用来存放每个左括号的下标，用于计算长度。



##### 代码

```javascript
var longestValidParentheses = function(s) {
  	//start记录合法括号序列的起始坐标
    let res=0, start=0;
    let stack=[];
    for(let i=0;i<s.length;i++){
        if(s[i]==='(')
            stack.push(i);
        else if(s[i]===')'){
          	//遇到右括号，但是栈内没有对应的左括号
          	//说明这是个不合法的括号，不会出现在目标序列里，将start往下移
            if(stack.length===0)
                start=i+1;
            else{
              	//匹配
                stack.pop();
              	//计算已成功匹配的合法括号序列长度
              	//根据栈内所剩元素分两类计算
              	//一类是‘（（））’,另一类为‘（（（））’
                res=stack.length===0?Math.max(res,i-start+1):Math.max(res,i-stack[stack.length-1]);
            }
        }
    }
    return res;
};
```



##### 总结

虽然是一道Hard的题目，但是难度感觉不是很大。思路上，如果对“【Leetcode 20】有效的括号”，还有印象的话，应该是很容易想到的。核心就是栈的运用。
