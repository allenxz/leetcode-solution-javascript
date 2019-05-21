##### 662. 二叉树最大宽度

给定一个二叉树，编写一个函数来获取这个树的最大宽度。树的宽度是所有层中的最大宽度。这个二叉树与**满二叉树（full binary tree）**结构相同，但一些节点为空。

每一层的宽度被定义为两个端点（该层最左和最右的非空节点，两端点间的`null`节点也计入长度）之间的长度。

**示例 1:**

```
输入: 

           1
         /   \
        3     2
       / \     \  
      5   3     9 

输出: 4
解释: 最大值出现在树的第 3 层，宽度为 4 (5,3,null,9)。
```

**示例 2:**

```
输入: 

          1
         /  
        3    
       / \       
      5   3     

输出: 2
解释: 最大值出现在树的第 3 层，宽度为 2 (5,3)。
```

**示例 3:**

```
输入: 

          1
         / \
        3   2 
       /        
      5      

输出: 2
解释: 最大值出现在树的第 2 层，宽度为 2 (3,2)。
```

**示例 4:**

```
输入: 

          1
         / \
        3   2
       /     \  
      5       9 
     /         \
    6           7
输出: 8
解释: 最大值出现在树的第 4 层，宽度为 8 (6,null,null,null,null,null,null,7)。
```

**注意:** 答案在32位有符号整数的表示范围内。



##### 解题思路

思路源自：

<<https://leetcode.com/problems/maximum-width-of-binary-tree/discuss/154200/JavaScript-DFS-solution>

每个孩子`index`，即左/右孩子在二叉树的整行中的位置，将是`2n`（左）或`2n+1`（右），其中n是父母的位置或索引。它从位置为0的根开始，它的左边是0，右边是1，依此类推......看起来像这样：

```
            0                     
     0           1
  0     1     2      3
 0 1   2 3   4 5    6 7 
```

1. 父母的每个最右节点都给出了该行的最大宽度。即使是空缺也同样成立。

2. 要跟踪子节点的索引是不够的，我们还需要知道深度。为此，引入一个零数组作为占位符 ：此数组的大小表示到目前为止看到的最大深度。

3. 接下来的步骤相当于做这样的转化

   ```
   输入: 
   
             1
            / \
           3   2
          /     \  
         5       9 
        /         \
       6           7   
       
       			↓
       			↓
       			
             0
            / \
           0   1
          /     \  
         0       1 
        /         \
       0           1
   ```

   



##### 代码

```javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number}
 */
var widthOfBinaryTree = function(root) {
    const min = [0];
    let max = 0;
    dfs(root, 0, 0);
    return max;

    function dfs(node, level, pos) {
    	if (!node) return;
    	if (level === min.length) {
      	left[level] = pos;
    	}

    	const delta = pos-min[level];
    	max = Math.max(max, delta+1);
    	dfs(node.left, level+1, delta*2);
    	dfs(node.right, level+1, delta*2+1);
    }
};
```

