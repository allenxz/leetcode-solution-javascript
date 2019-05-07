> “I love you three thousand times”



##### 19. 删除链表的倒数第N个节点

给定一个链表，删除链表的倒数第 *n* 个节点，并且返回链表的头结点。

**示例：**

```
给定一个链表: 1->2->3->4->5, 和 n = 2.

当删除了倒数第二个节点后，链表变为 1->2->3->5.
```

**说明：**

给定的 *n* 保证是有效的。



##### 解题思路

这道题比较经典，我们设置两个指针就行，让一个指针先走n步，然后第二个指针再出发，这样等第一个指针到达链表末端时，第二个指针正好指向要删除结点的前一个结点。至于为什么是前一个结点，emmm...链表删除的常规操作。注意的是我们可以给链表加一个头结点，然后再继续操作，这样处理“删除结点是第一个结点“时比较方便。



##### 代码

```javascript
var removeNthFromEnd = function(head, n) {
    let res=new ListNode();
    res.next=head;
    let first=second=res;
    let cnt=0;
    while (first.next!=null){
        cnt++;
        if(cnt>n){
            second=second.next;
        }
        first=first.next;
    }
    second.next=second.next.next;
    return res.next;
};
```



##### 总结

链表类型的题目里也常常用到指针，多往这方面想想。