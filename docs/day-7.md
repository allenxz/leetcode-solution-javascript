> 今天是道easy的题目，比较轻松



##### 7. 整数翻转

给出一个 32 位的有符号整数，你需要将这个整数中每位上的数字进行反转。

**示例 1:**

```
输入: 123
输出: 321
```

 **示例 2:**

```
输入: -123
输出: -321
```

**示例 3:**

```
输入: 120
输出: 21
```

**注意:**

假设我们的环境只能存储得下 32 位的有符号整数，则其数值范围为 [−2^31,  2^31 − 1]。请根据这个假设，如果反转后整数溢出那么就返回 0。



##### 解题思路

这个思路很简单，分析我直接写在代码了，这样容易看点。



##### 代码

```javascript
var reverse = function(x) {
    let res=0;
  	//给x留个备份，后面判断正反时候得用
    let tmp=x;
  	//统一转换成整数处理
    x=x<0?-x:x;
  	//反转
    while(x){
      	//取出x的最后一位加到res的第一位上
        res=res*10+x%10;
        //去掉x中已经被取出的最后一位数字
        x=Math.floor(x/10);
    }
    //如果是负数的话，将符号补上
    if(tmp<0)
        res=-res;
  	//−2^31=-2147483648, 2^31−1=2147483647
  	//处理溢出情况
    if(res>2147483647||res<-2147483648)
        return 0;
    else
        return res;
};
```



##### 总结

emmm……没什么好总结的这个，需要注意的就是处理溢出了，其他的都比较简单。好好学习，天天向上。

