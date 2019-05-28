##### 739. 每日温度

根据每日 `气温` 列表，请重新生成一个列表，对应位置的输入是你需要再等待多久温度才会升高的天数。如果之后都不会升高，请输入 `0` 来代替。

例如，给定一个列表 `temperatures = [73, 74, 75, 71, 69, 72, 76, 73]`，你的输出应该是 `[1, 1, 4, 2, 1, 1, 0, 0]`。

**提示：**`气温` 列表长度的范围是 `[1, 30000]`。每个气温的值的都是 `[30, 100]` 范围内的整数。



##### 解题思路

我们用一个递减栈去记录每天的气温情况(实际上，栈内放的是下标)。整个栈按气温降序排列。

首先遍历数组：

* 当前元素如果大于栈顶元素，栈顶元素出栈，并计算下标的差值，并给给新列表的相应地方赋值

* 当前元素如果小于栈顶元素，当前元素入栈

  

##### 代码

```javascript
/**
 * @param {number[]} T
 * @return {number[]}
 */
var dailyTemperatures = function(T) {
    let stack=[];
    let res=new Array(T.length).fill(0);
    for(let i=0;i<T.length;i++){
        if(stack){
            while(stack&&T[stack[stack.length-1]]<T[i]){
                res[stack[stack.length-1]]=i-stack[stack.length-1];
                stack.pop();
            }
        }
        stack.push(i);
    }
    return res;
};
```
