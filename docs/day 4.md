> 好像要下雨了...



#### 4. 寻找两个有序数组的中位数

给定两个大小为 m 和 n 的有序数组 `nums1` 和 `nums2`。

请你找出这两个有序数组的中位数，并且要求算法的时间复杂度为 O(log(m + n))。

你可以假设 `nums1` 和 `nums2` 不会同时为空。

**示例 1:**

```
nums1 = [1, 3]
nums2 = [2]

则中位数是 2.0
```

**示例 2:**

```
nums1 = [1, 2]
nums2 = [3, 4]

则中位数是 (2 + 3)/2 = 2.5
```



#### 解题思路

真的不愧是hard难度的题。虽然题目说了时间复杂度是O(log(m + n))，已经明示了要用分治法。可想了很久还是不得道。看了官方题解，那是真的流批。既然珠玉在前，我就不献丑了。下面有官方题解的链接。强烈推荐看看，说的很仔细。

https://leetcode-cn.com/problems/median-of-two-sorted-arrays/solution/



#### 代码

```javascript
var findMedianSortedArrays = function(nums1, nums2) {
    let m=nums1.length;
    let n=nums2.length;
    // 确保n>=m，且nums2中放的是较长的数组
    if(m>n){
        let tmp=nums1;
        nums1=nums2;
        nums2=tmp;
        tmp=m;
        m=n;
        n=tmp;
    }
  	//关键是在[0,m]中找到那个合适的i，j是伴随i变化的值
    let iMin=0,iMax=m,halfLen=Math.floor((m+n+1)/2);
    while (iMin<=iMax){
        let i=Math.floor((iMin+iMax)/2);
        let j=halfLen-i;
      	//i太小
        if(i<iMax&&nums2[j-1]>nums1[i]){
            iMin=i+1;
        }
      	//i太大
        else if (i>iMin&&nums1[i-1]>nums2[j]) {
            iMax=i-1;
        }
      	//合适的i
        else{
            let maxLeft=0;
            //考虑边界情况,nums1[i-1]或nums2[j-1]不存在
            if(i===0) {
                maxLeft =nums2[j-1];
            }
            else if(j===0) {
                maxLeft =nums1[i-1];
            }
            //一般情况
            else {
                maxLeft =Math.max(nums1[i-1],nums2[j-1])
            }
            //总长度为奇数时
            if((m+n)%2===1){
                return maxLeft;
            }

            let minRight=0;
            //考虑边界情况,nums1[i]或nums2[j]不存在
            if(i===m) {
                minRight =nums2[j];
            }
            else if(j===n) {
                minRight =nums1[i];
            }
            //一般情况
            else {
                minRight =Math.min(nums1[i],nums2[j])
            }
            //总长度为偶数时
            return (maxLeft+minRight)/2.0;
        }
    }
};
```



#### 总结

> 中位数：将一个集合划分为两个长度相等的子集，其中一个子集中的元素总是大于另一个子集中的元素。

这个概念真的是醍醐灌顶。直接引导了整个算法的思路。



这道题的关键就是找到一条”线“，将这两个数组划成来两个部分。

```markdown
 					left_part          |        right_part
    A[0], A[1], ..., A[i-1]  |  A[i], A[i+1], ..., A[m-1]
    B[0], B[1], ..., B[j-1]  |  B[j], B[j+1], ..., B[n-1]
```

当这样的划分满足下面两个条件：
$$
len(\text{left_part})=len(\text{left_part})\\
max(\text{left_part})≤min(\text{left_part})
$$
就有：	
$$
median= \frac{max(\text{left_part})+min(\text{left_part})}{2}
$$


分治法则是用在寻找那条线，也就是i的合适值。

一开始`i∈[0,m]`，通过`B[j-1]≤A[i]`和`A[i-1]≤B[j]`（即条件②）进行判断，不符合的就进行相应的调整，直到找到同时符合的，即合适的i。