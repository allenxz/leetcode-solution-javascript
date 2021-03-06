> 一个月，时间过得有点快



##### 38. 报数

报数序列是一个整数序列，按照其中的整数的顺序进行报数，得到下一个数。其前五项如下：

```
1.     1
2.     11
3.     21
4.     1211
5.     111221
```

`1` 被读作  `"one 1"`  (`"一个一"`) , 即 `11`。
`11` 被读作 `"two 1s"` (`"两个一"`）, 即 `21`。
`21` 被读作 `"one 2"`,  "`one 1"` （`"一个二"` ,  `"一个一"`) , 即 `1211`。

给定一个正整数 *n*（1 ≤ *n* ≤ 30），输出报数序列的第 *n* 项。

注意：整数顺序将表示为一个字符串。

 

**示例 1:**

```
输入: 1
输出: "1"
```

**示例 2:**

```
输入: 4
输出: "1211"
```



##### 解题思路

这道题题目不难，但是有点不好读懂题意。

我翻译一下，报数序列的第一项为`1`，后面的每一项都对前一项进行报数，即描述前一项中每个数字连续出现了多少次，所以：

第二项为`11`，因为第一项只有一个1；

第三项为`21`，因为第二项有两个1；

第四项为`1211`，因为第三项有一个2和一个1;

依次类推......

知道思路以后，问题就转化成了类似于记录字符串内数字连续次数情况的题目，就很简单了。



##### 代码

```javascript
var countAndSay = function(n) {
  	//初始化第一项
    let res='1';
    if(n===1)
        return res;
    for(let i=2;i<=n;i++){
      	//word辅助判断该数字是否连续重复出现
      	//cnt记录次数
      	//tmp记录报数序列的新项
        let word=res[0],cnt=0,tmp='';
        for(let j=0;j<res.length;j++){
            if(word===res[j])
                cnt++;
            else{
                tmp+=cnt+word
                word=res[j];
                cnt=1;
            }
        }
      	//记得处理最后一次的情况
        tmp+=cnt+word;
        res=tmp;
    }
    return res;
};
```



##### 总结

读懂题意，然后对问题进行转化很重要。
