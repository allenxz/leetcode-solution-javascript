> go on 



##### 17. 电话号码的字母组合

给定一个仅包含数字 `2-9` 的字符串，返回所有它能表示的字母组合。

给出数字到字母的映射如下（与电话按键相同）。注意 1 不对应任何字母。

![](../images/200px-Telephone-keypad2.svg.png)

**示例:**

```
输入："23"
输出：["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
```

**说明:**
尽管上面的答案是按字典序排列的，但是你可以任意选择答案输出的顺序。



##### 解题思路

像是这种求组合数且解较多的题目，一般我们用回溯算法。

回溯算法，通俗的来说就是，先一条路走到黑，遇到死胡同了再退一步，换另外一条路继续走到黑，直到走遍所有的路。

回溯算法的一般递归模板如下：

```c++
void backtracking(int 当前状态)  
{  
      if(当前状态为边界状态)  
      {  
        记录或输出  
        return;  
      }  
      for(i=0;i<n;i++) //横向遍历解答树所有子节点  
      {  
           //扩展出一个子状态。  
           修改了全局变量  
           if(子状态满足约束条件)  
            {  
              backtracking(子状态)  
           }  
            恢复全局变量//回溯部分  
      }  
}  
```



##### 代码

```javascript
var backtracking = function (res,tmp,digits,map,k) {
    if(tmp.length===digits.length){
        res.push(tmp);
    }
    else{
        for(let i=0;i<map.get(digits[k]).length;i++){
            tmp+=map.get(digits[k])[i];
          	//更新子状态，往深处递归
            backtracking(res,tmp,digits,map,k+1);
          	//回溯
            tmp=tmp.slice(0,tmp.length-1);
        }
    }
}

var letterCombinations = function(digits) {
    let map=new Map([
        ['2','abc'],['3','def'],['4','ghi'],['5','jkl'],['6','mno'],['7','pqrs'],['8','tuv'],['9','wxyz']
    ]);
    let res=[];
    if(digits.length===0)
        return res;
    backtracking(res,'',digits,map,0);
    return res;
};
```



##### 总结

回溯算法说白了就是穷举法。不过回溯算法使用剪枝函数，剪去一些不可能到达最终状态（即答案状态）的节点，从而减少状态空间树节点的生成。 
回溯法是一个既带有系统性又带有跳跃性的的搜索算法。它在包含问题的所有解的解空间树中，按照深度优先的策略，从根结点出发搜索解空间树。算法搜索至解空间树的任一结点时，总是先判断该结点是否肯定不包含问题的解。如果肯定不包含，则跳过对以该结点为根的子树的系统搜索，逐层向其祖先结点回溯。否则，进入该子树，继续按深度优先的策略进行搜索。

* 回溯法在用来求问题的所有解时，要回溯到根，且根结点的所有子树都已被搜索遍才结束。

* 而回溯法在用来求问题的任一解时，只要搜索到问题的一个解就可以结束。



思路源自以下链接：

https://blog.csdn.net/crystal6918/article/details/51924665

https://blog.csdn.net/fengchi863/article/details/80086915

https://blog.csdn.net/wonner_/article/details/80373871