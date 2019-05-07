> 



##### 30.  串联所有单词的子串

给定一个字符串 **s** 和一些长度相同的单词 **words。**找出 **s** 中恰好可以由 **words** 中所有单词串联形成的子串的起始位置。

注意子串要与 **words** 中的单词完全匹配，中间不能有其他字符，但不需要考虑 **words** 中单词串联的顺序。

 

**示例 1：**

```
输入：
  s = "barfoothefoobarman",
  words = ["foo","bar"]
输出：[0,9]
解释：
从索引 0 和 9 开始的子串分别是 "barfoor" 和 "foobar" 。
输出的顺序不重要, [9,0] 也是有效答案。
```

**示例 2：**

```
输入：
  s = "wordgoodgoodgoodbestword",
  words = ["word","good","best","word"]
输出：[]
```



##### 解题思路

我直接用暴力解的，讨论区有用自动机之类去解的，很牛逼，有兴趣可以去看看。

由于是暴力求解的，思路写在解释里的，比较好理解。



##### 代码

```javascript
var findSubstring = function(s, words) {
    let res=[];
  	//处理特殊情况
    if(s.length===0||words.length===0||s.length<words[0].length*words.length)
        return res;
    let map=new Map();
  	//将words数组转成Map，key为word，value为出现次数
    for(let i=0;i<words.length;i++){
        if(map.has(words[i]))
            map.set(words[i],map.get(words[i])+1);
        else
            map.set(words[i],1);
    }
  	//记录每个单词的长度
    let len=words[0].length;
  	//记录所有单词串联后的长度
    let totalLen=len*words.length;
    for(let i=0;i+totalLen-1<s.length;i++){
      	//从s中逐段截出totalLen长的子串
        let str=s.substring(i,i+totalLen);
      	//拷贝一份map，用于检测子串是否包含了所有单词
        let tmp=new Map(map);
      	//将子串截成len长的若干个小段，逐一判断是否是需要的单词
        for(let j=0;j<totalLen;j=j+len){
            let word=str.substring(j,j+len);
            if(!tmp.has(word))
                break;
            if(tmp.get(word)===1)
                tmp.delete(word);
            else
                tmp.set(word,tmp.get(word)-1);
        }
      	//拷贝出来的map为空，说明该子串包含了所有所需单词
        if(tmp.size===0)
            res.push(i);
    }
    return res;
};
```



##### 总结

这里有个小坑，拷贝map必须得是深拷贝，不然的话在改变tmp的时候，map也会变化。

而我在Day 1的时候，有总结过一些map的js使用方法。但是我才发现，之前我写的那种实际是通过Object模拟的Map，实现深拷贝的话得写函数去处理，而且很复杂。所以我这道题用的是es6后js新加的Map对象。具体的属性和方法下面的链接有。

https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Map