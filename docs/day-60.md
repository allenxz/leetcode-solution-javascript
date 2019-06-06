##### 451. 根据字符出现频率排序

给定一个字符串，请将字符串里的字符按照出现的频率降序排列。

**示例 1:**

```
输入:
"tree"

输出:
"eert"

解释:
'e'出现两次，'r'和't'都只出现一次。
因此'e'必须出现在'r'和't'之前。此外，"eetr"也是一个有效的答案。
```

**示例 2:**

```
输入:
"cccaaa"

输出:
"cccaaa"

解释:
'c'和'a'都出现三次。此外，"aaaccc"也是有效的答案。
注意"cacaca"是不正确的，因为相同的字母必须放在一起。
```

**示例 3:**

```
输入:
"Aabb"

输出:
"bbAa"

解释:
此外，"bbaA"也是一个有效的答案，但"Aabb"是不正确的。
注意'A'和'a'被认为是两种不同的字符。
```



##### 解题思路

首先用一个Map记录每个字符的出现频次，然后用`Array.from`方法把Map转出数组。然后根据字符的出现频次从大到小排序。最后再遍历排序后的数组，按照顺序加入和频次相等的对应字符就行。



##### 代码

```javascript
var frequencySort = function(s) {
    let map=new Map();
    for(let i=0;i<s.length;i++){
        if(map.has(s[i])){
            map.set(s[i],map.get(s[i])+1);
        }
        else{
            map.set(s[i],1);
        }
    }
    var arr=Array.from(map);
    arr.sort((a,b)=>{
        return b[1]-a[1];
    });
    let res=[];
    for(let i=0;i<arr.length;i++){
        for(let j=0;j<arr[i][1];j++)
            res.push(arr[i][0]);
    }
    return res.join('');
};
```

##### 

