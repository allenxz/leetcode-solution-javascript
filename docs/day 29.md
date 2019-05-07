##### 39.  解数独

编写一个程序，通过已填充的空格来解决数独问题。

一个数独的解法需**遵循如下规则**：

1. 数字 `1-9` 在每一行只能出现一次。
2. 数字 `1-9` 在每一列只能出现一次。
3. 数字 `1-9` 在每一个以粗实线分隔的 `3x3` 宫内只能出现一次。

空白格用 `'.'` 表示。

![img](../images/250px-Sudoku-by-L2G-20050714.svg (1).png)

一个数独。

![img](../images/250px-Sudoku-by-L2G-20050714_solution.svg.png)

答案被标成红色。

**Note:**

- 给定的数独序列只包含数字 `1-9` 和字符 `'.'` 。
- 你可以假设给定的数独只有唯一解。
- 给定数独永远是 `9x9` 形式的。



##### 解题思路

这道题就是昨天那道题的进阶版，思路是一脉相承的。

难度增加在于这道题你得去回溯，就跟你做数独一样，先假设填一个数，然后往下，直到你遇到死胡同了，再退回来，换一个数。具体的见注释。



##### 代码

```javascript
/**
 * @param {character[][]} board
 * @return {void} Do not return anything, modify board in-place instead.
 */
var solveSudoku = function(board) {
  	//下面3个二维数组分别记录每行/列/格的数字使用情况
    let row=new Array(9);
    let col=new Array(9);
    let grid=new Array(9);
    for(let i=0;i<9;i++){
        row[i]=new Array(10);
        col[i]=new Array(10);
        grid[i]=new Array(10);
    }
  	//用已填充的部分，初始3个二维数组
    for(let i=0;i<9;i++){
        for(let j=0;j<9;j++){
            if(board[i][j]!=='.'){
                let num=board[i][j]-'0';
                row[i][num]=true;
                col[j][num]=true;
                let index=(i/3|0)*3+(j/3|0);
                grid[index][num]=true;
            }
        }
    }
  	//从数独的第一个格子进行深搜
    dfs(0, 0);
    
  	//深搜函数
    function dfs(i,j){
      	//找到未填充的空格
        while(board[i][j]!=='.'){
            if(++j>=9){
                i++;
                j=0;
            }
            if(i>=9)
                return true;
        }
      	//从0~9开始假设性放数字
        for(let num=1;num<=9;num++){
            let index=(i/3|0)*3+(j/3|0);
          	//当前数字没被使用，暂时填下去
            if(!row[i][num]&&!col[j][num]&&!grid[index][num]){
                board[i][j]=num+'';
                row[i][num]=true;
                col[j][num]=true;
                grid[index][num]=true;
              	//更新子状态，往深递归
                if(dfs(i,j))
                    return true;
              	//该子状态不是有效的数独，回溯
                else{
                    row[i][num]=false;
                    col[j][num]=false;
                    grid[index][num]=false;
                    board[i][j]='.';
                }
            }
        }
      	//9个数字都无法填，说明当前子状态不符合
        return false;
    }
};
```



##### 总结

总而言之是一道深搜+数学（little）的题目，回溯的话按照模板写就好，之前我总结过了就不多说了。还得写别的，溜惹。

