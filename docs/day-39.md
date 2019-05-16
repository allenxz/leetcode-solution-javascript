##### 223.  矩形面积

在**二维**平面上计算出两个**由直线构成的**矩形重叠后形成的总面积。

每个矩形由其左下顶点和右上顶点坐标表示，如图所示。

![Rectangle Area](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/10/22/rectangle_area.png)

**示例:**

```
输入: -3, 0, 3, 4, 0, -1, 9, 2
输出: 45
```

**说明:** 假设矩形面积不会超出 **int** 的范围。



##### 解题思路

这道题好像有一次蓝桥杯考了类似的题目。思路和数学里的韦恩图算集合交并补什么的有点像。

总面积=两个矩形面积之和-重叠部分面积



##### 代码

```javascript
/**
 * @param {number} A
 * @param {number} B
 * @param {number} C
 * @param {number} D
 * @param {number} E
 * @param {number} F
 * @param {number} G
 * @param {number} H
 * @return {number}
 */
var computeArea = function(A, B, C, D, E, F, G, H) {
    let s1=(C-A)*(D-B);
    let s2=(G-E)*(H-F);
    let height=Math.min(D,H)-Math.max(B,F);
    let width=Math.min(G,C)-Math.max(E,A);
    let s3;
    if(height>0&&width>0)
        s3=height*width;
    else
        s3=0;
    return s1+s2-s3;
};
```
