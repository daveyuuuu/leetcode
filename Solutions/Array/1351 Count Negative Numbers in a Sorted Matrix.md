**题目理解**

- 给定一个$m\times n$的矩阵，每一行每一列都是非递增排列，求矩阵中的负数的个数

**思考过程**

1. 直接遍历整个矩阵，对负数进行计数，见法一

2. 因为矩阵每一列每一行都是非递增的，因此只要找到一个负数，它的下面或右边全是负数，因此考虑从右上角开始找起，如果为负，则加上这一列剩余的负数，继续向左边寻找，若为正，说明左边全是正数，此时向下面寻找，直到达到边界值，见法二

**具体代码**

法一
```javascript
var countNegatives = function(grid) {
  let result = 0
  for (let i = 0; i < grid.length; ++i) {
    for (let j = 0; j < grid[i].length; ++j) {
      if (grid[i][j] < 0) {
        result++
      }
    }
  }
  return result
}
```

法二
```javascript
var countNegatives = function(grid) {
  let result = 0
  let n = grid.length
  let col = grid[0].length - 1
  let row = 0
  while(row < n && col >= 0) {
    if (grid[row][col] < 0) {
      result += n - row
      col--
    } else {
      row++
    }
  }
  return result
}
```

