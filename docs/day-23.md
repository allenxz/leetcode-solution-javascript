##### 29. 两数相除

给定两个整数，被除数 `dividend` 和除数 `divisor`。将两数相除，要求不使用乘法、除法和 mod 运算符。

返回被除数 `dividend` 除以除数 `divisor` 得到的商。

**示例 1:**

```
输入: dividend = 10, divisor = 3
输出: 3
```

**示例 2:**

```
输入: dividend = 7, divisor = -3
输出: -2
```

**说明:**

- 被除数和除数均为 32 位有符号整数。
- 除数不为 0。
- 假设我们的环境只能存储 32 位有符号整数，其数值范围是 [−2^31,  2^31 − 1]。本题中，如果除法结果溢出，则返回 231 − 1。



##### 解题思路

首先我们想到的是用减法模拟除法，我们算被除数可以被多少个除数减去就能得到商。当然我们可能一个一个除数去减，我们可以用2的n次方个除数，n从0开始递增，这样能迅速削减被除数。

我做完之后发现讨论区大神有用位运算去做的，那样的话会比减法来的快，但是js的位运算只适用于32位整数。

所以当被除数为最小值的时候会出错。暂时没想到怎么优化，先放一边。



##### 代码

```javascript
var divide = function(dividend, divisor) {
    let result = 0, sign = 1, mul = 1;
  	//判断商的符号
    if ((dividend > 0 && divisor < 0) || (dividend < 0 && divisor > 0)) {
        sign = -1;
    }
    dividend = Math.abs(dividend);
    divisor = Math.abs(divisor);
 
    let divisor2 = divisor;
 
  	//dividend =divisor*2^n + …… + divisor*2^2 + divisor*2^1 + divisor*2^0
  	//mul即2^n(n>=1)
    while (dividend >= divisor2) {
        if (dividend > (divisor2 + divisor2)) {
            divisor2 += divisor2;
            mul += mul;
        }
        dividend -= divisor2;
        result += mul;
    }
    while (dividend >= divisor) {
        dividend -= divisor;
        result += 1;
    }
 
  	//超出范围
    if (sign == 1 && result > (Math.pow(2, 31) - 1)) {
        return Math.pow(2, 31) - 1;
    } else if (sign == -1 && result < -Math.pow(2, 31)) {
        return -Math.pow(2, 31);
    }
    return sign>0?result:-result;
};
```



##### 总结

位运算的话本质上也是通过减法来模拟除法，且位运算对于算2的n次方这类的问题很是简便，所以代码就很优雅。

```java
 public int divide(int dividend, int divisor) {
        if (dividend == 0) {
            return 0;
        }
        if (dividend == Integer.MIN_VALUE && divisor == -1) {
            return Integer.MAX_VALUE;
        }
        boolean negative;
        negative = (dividend ^ divisor) <0;//用异或来计算是否符号相异
        long t = Math.abs((long) dividend);
        long d= Math.abs((long) divisor);
        int result = 0;
        for (int i=31; i>=0;i--) {
            if ((t>>i)>=d) {//找出足够大的数2^n*divisor
                result+=1<<i;//将结果加上2^n
                t-=d<<i;//将被除数减去2^n*divisor
            }
        }
        return negative ? -result : result;//符号相异取反
    }
```

