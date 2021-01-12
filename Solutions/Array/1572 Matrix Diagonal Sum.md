**题目理解**

- 给定一个矩阵，计算的主对角线和副对角线的和，中间的值只计算一次。

**思考过程**

1. 按照题意分别遍历主副对角线，然后求和即可，见法一

**具体代码**

法一
```javascript
var diagonalSum = function(mat) {
  const n = mat.length
  let result = 0
  for (let i = 0, j = 0; i < n && j < n; ++i, ++j) {
    result += mat[i][j]
  }
  for (let i = 0, j = n-1; i < n && j >= 0; ++i, --j) {
    if (i === j) {
      continue
    } else {
      result += mat[i][j]
    }
  }
  return result
}
```
