> ...8多说，直接冲



##### 23. 合并K个排序链表

合并 *k* 个排序链表，返回合并后的排序链表。请分析和描述算法的复杂度。

**示例:**

```
输入:
[
  1->4->5,
  1->3->4,
  2->6
]
输出: 1->1->2->3->4->4->5->6
```



##### 解题思路

首先这道题有个很猥琐的做法，就是依次遍历所有的链表中的元素，然后装在一个数组里，排好序后再把数组里的所有元素塞到一个新的链表里。理论上这样的时间复杂度也是O(n)，应该是能跑的过的，我也没试，毕竟太猥琐了。

我们说个正经的思路，k个有序链表的合并，我们很自然就会想到两个两个去合并，因为实际上我们亲自去做的话也是这样的。

而这样的思路就是归并（也就是分治法的思想）。将全部链表分成左右两部分，然后每部分再平分，直到每部分只剩下两个链表，我们将其

合并然后返回。

##### 代码

```javascript
//合并两个有序链表
var mergeTwoLists = function(l1, l2) {
    if(l1 == null)
        return l2;

    if(l2 == null)
        return l1;


    if(l1.val >= l2.val) {
        l2.next = mergeTwoLists(l1, l2.next);
        return l2;
    }
    else {
        l1.next = mergeTwoLists(l1.next, l2);
        return l1;
    }
};
//归并
var merge = function(l,r,lists){
    let m=(l+r)/2 | 0;
    if(l===r)
        return lists[l];
    let u=merge(l,m,lists);
    let v=merge(m+1,r,lists);
    return mergeTwoLists(u,v);
}
//主程序
var mergeKLists = function(lists) {
    if(lists.length===0)
        return null;
    else
        return merge(0,lists.length-1,lists);
    
};
```



##### 总结

分治法的就是将问题的复杂度不断降低，直到一个很小的维度，我们能轻易的求出解，一旦这个最小的维度上的解求出了，整个的解就可多通过若干个子问题的解组合而成。

此外我还学会了个新的小技巧，之前在js里面取整我都是用Math.floor，现在我发现用`| 0`能做到同样的效果，而且优雅很多。