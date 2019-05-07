> 一周过得好快，又到周六了



##### 6. z字形变换

将一个给定字符串根据给定的行数，以从上往下、从左到右进行 Z 字形排列。

比如输入字符串为 `"LEETCODEISHIRING"` 行数为 3 时，排列如下：

```markdown
L   C   I   R
E T O E S I I G
E   D   H   N
```

之后，你的输出需要从左往右逐行读取，产生出一个新的字符串，比如：`"LCIRETOESIIGEDHN"`。

请你实现这个将字符串进行指定行数变换的函数：

```markdown
string convert(string s, int numRows);
```

**示例 1:**

```markdown
输入: s = "LEETCODEISHIRING", numRows = 3
输出: "LCIRETOESIIGEDHN"
```

**示例 2:**

```markdown
输入: s = "LEETCODEISHIRING", numRows = 4
输出: "LDREOEIIECIHNTSG"
解释:

L     D     R
E   O E   I I
E C   I H   N
T     S     G
```



##### 解题思路

**方法一：**

题比较简单，我们一开始先创建一个长度为numRows的数组tmp，存变换后的每一行的字符串。

拿示例2举例，tmp[0]='LDR'，tmp[1]='EOEII'，后面的依次类推。

然后我们去遍历字符串s，将每个字符放到他们该在的行上。而且我们很容易发现，它按z字形去放，相当于一个指针j，先从0递增遍历到numrows-1，然后再从numrows-1递减遍历到0。

这样做的时间复杂度是O(n)，空间复杂度的话使用了一个数组，所以也是O(n)。



**方法二：**

那其实我们也有办法去减少这个数组的开销，将时间复杂度降到O(1)（不算上返回字符串的空间）。

我们可以直接按照与逐行读取 Z 字形图案相同的顺序访问字符串。

对于所有整数 k，

- 行 0 中的字符位于索引 k  （**2⋅numRows−2**） 处;
- 行 numRows−1 中的字符位于索引 k （**(2⋅numRows−2)+numRows−1**）处;
- 内部的 行 i 中的字符位于索引 k（**(2⋅numRows−2)+i**）以及 (k+1)（**(2⋅numRows−2)−i**）处;



##### 代码

```javascript
//方法1
var convert = function(s, numRows) {
    if(numRows===1) return s;
    let tmp=new Array(numRows).fill('');
    let flag=-1;
    for(let i=0,j=0;i<s.length;i++){
        if(j===numRows-1||j===0)
            flag*=-1;
        tmp[j]+=s[i];
        j+=flag;
    }
    let res='';
    for(let i=0;i<numRows;i++){
        res+=tmp[i];
    }
    return res;
};

//方法2
var convert = function(s, numRows) {
    if (numRows===1) return s;
    let res='';
    let n = s.length;
    let cycleLen = 2 * numRows - 2;

    for (let i = 0; i < numRows; i++) {
        for (let j = 0; j + i < n; j += cycleLen) {
            res+=s[j+i];
            if (i !== 0 && i !== numRows - 1 && j + cycleLen - i < n)
                res+=s[j+cycleLen-i];
        }
    }
    return res;
};
```



##### 总结

这道题的难度是Medium。类似这种题，其实看懂题意就挺好解决的。题型上面类似于模拟。

