> 赶了一晚的需求，自古甲方是爸爸。



##### 39. 组合总和

给定一个**无重复元素**的数组 `candidates` 和一个目标数 `target` ，找出 `candidates` 中所有可以使数字和为 `target` 的组合。

`candidates` 中的数字可以无限制重复被选取。

**说明：**

- 所有数字（包括 `target`）都是正整数。
- 解集不能包含重复的组合。 

**示例 1:**

```
输入: candidates = [2,3,6,7], target = 7,
所求解集为:
[
  [7],
  [2,2,3]
]
```

**示例 2:**

```
输入: candidates = [2,3,5], target = 8,
所求解集为:
[
  [2,2,2,2],
  [2,3,3],
  [3,5]
]
```



##### 解题思路

这道题和前面的回溯算法的题目都很像，思路基本一样，难点我个人觉得是在深拷贝，如果只是浅拷贝的话，会影响上层递归。老样子，思路写注释里。



##### 代码

```javascript
var combinationSum = function(candidates, target) {
    let res=[];
    let list=[];
  	//排个序
    candidates.sort(function (a,b){
        return a-b;
    });
  	//开始递归
    find(list,target,0);
    return res;
    function find(tmp,target,num){
      	//递归出口，target为0说明tmp为合适的确定解
        if(target===0){
            res.push(tmp);
            return;
        }
      	//target比最小的数都小，说明解到这一步陷入死胡同了，回溯
        if(target<candidates[0])
            return;
      
        for(let i=num;i<candidates.length&&candidates[i]<=target;i++){
          	//深拷贝原本的待定解
            let list=tmp.concat();
          	//将寻找到的合适数字，放进list中形成新的待定解
            list.push(candidates[i]);
          	//往深处递归
            find(list,target-candidates[i],i);
        }
    }
};
```



##### 总结

js数组的深拷贝方法：`let list=tmp.concat();`

