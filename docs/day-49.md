##### 287. 寻找重复数

给定一个包含 *n* + 1 个整数的数组 *nums*，其数字都在 1 到 *n* 之间（包括 1 和 *n*），可知至少存在一个重复的整数。假设只有一个重复的整数，找出这个重复的数。

**示例 1:**

```
输入: [1,3,4,2,2]
输出: 2
```

**示例 2:**

```
输入: [3,1,3,4,2]
输出: 3
```

**说明：**

1. **不能**更改原数组（假设数组是只读的）。
2. 只能使用额外的 *O*(1) 的空间。
3. 时间复杂度小于 *O*(*n*2) 。
4. 数组中只有一个重复的数字，但它可能不止重复出现一次。



##### 解题思路

这道题其实如果没有限制条件的话很简单。但是加上限制条件之后，真的很难想。听说国外的某个计算机大神都用了24小时才解出来...

思路参考：<https://leetcode.com/problems/find-the-duplicate-number/discuss/72846/My-easy-understood-solution-with-O(n)-time-and-O(1)-space-without-modifying-the-array.-With-clear-explanation.>



我们把数组看作是链表，将数组的下标和里面放置的元素结合起来，形成一个含环的链表。

举个例子：从nums[0]即1开始，下一个元素为nums[nums[0]]即3，后面的依次类推，结果为：

[1,3,4,2,2]转换为1->3->2->4->2->4

将问题转换成寻找链表环的入口点。而链表判环问题，我们通过快慢指针去做。

但是快慢指针只能判断链表有没有环，找出重复元素的话还是比较复杂。我们先看代码。



##### 代码

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var findDuplicate = function(nums) {
    let slow = nums[0];
    let fast = nums[nums[0]];
    while (slow!==fast){
        slow = nums[slow];
        fast = nums[nums[fast]];
    }
    fast = 0;
    while (fast!==slow){
        fast = nums[fast];
        slow = nums[slow];
    }
    return slow;
};
```



##### 总结

结合代码我们看一个数学证明过程：

假设相遇时慢指针移动了s，则快指针移动了2s，设圆圈的长度为c，n为周期，

则有：2s=s+n*c

等价于：s=n*c  (1)；

接着假设链表的起点到环的入口点的距离为x，从入口到相遇点的距离为a

则有：s=x+a  (2);

由(1)和(2)得：

s=n*c=x+a

=>x+a=(n-1)*c+c

=>x=(n-1)*c+c-a

c-a表示相遇点到入口的距离

所以等式的左边意义为：某个新指针从起点走了x的距离

等式的右边意义为：慢指针在环里移动了(n-1)周，加上相遇点到入口的距离。

所以新指针和慢指针相遇的位置就是入口点，即重复元素。