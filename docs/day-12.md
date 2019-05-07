> 又到了周五，愉快的周末又来惹



##### 14. 最长公共前缀

编写一个函数来查找字符串数组中的最长公共前缀。

如果不存在公共前缀，返回空字符串 `""`。

**示例 1:**

```
输入: ["flower","flow","flight"]
输出: "fl"
```

**示例 2:**

```
输入: ["dog","racecar","car"]
输出: ""
解释: 输入不存在公共前缀。
```

**说明:**

所有输入只包含小写字母 `a-z` 。



##### 解题思路

首先我们将字符串数组中的第一位定为res即公共前缀，按照例子来说的话，此时` res='flower' ‘。

然后用这个公共前缀去检测字符串数组的其他字符串，看其他字符串中是否包含该前缀：

​	包含的话就继续下一个字符串检测；

​	不包含就去掉前缀的最后一位，然后继续检测，直到包含或者前缀被删光（即res为空字符串，表示没有公共前缀）。



##### 代码

```javascript
var longestCommonPrefix = function(strs) {
    if(strs.length===0)
        return '';
    let res=strs[0];
    for(let i=0;i<strs.length;i++){
        while (strs[i].indexOf(res)) {
            res=res.substring(0,res.length-1);
            if(res.length===0)
                return '';
        }
    }
    return res;
};
```



##### 总结

这道题的难度为Easy，思路也比较容易。就不多说了，掰。明天见~