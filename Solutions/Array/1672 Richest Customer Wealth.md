**题目理解**

- 给定一个$m\times n$的矩阵，矩阵的第i行，第j列代表第i位用户在第j个银行的存款，返回存款最多的用户的存款数额

**思考过程**

1. 按照题意，即矩阵的每一行的和代表该行用户的所有存款，遍历每一行并求和，记录最大的即可，见法一

2. JS风格的做法，见法二

**具体代码**

法一
```javascript
var maximumWealth = function(accounts) {
    const m = accounts.length
    const n = accounts[0].length 
    let result = 0
    for (let i = 0; i < m; ++i) {
      let temp = 0
      for (let j = 0; j < n; ++j) {
        temp += accounts[i][j]
      }
      result = temp > result ? temp : result
    }
    return result
}
```

法二
```javascript
var maximumWealth = function(accounts) {
  return Math.max(...accounts.map(arr => arr.reduce((acc, cur) => acc + cur)))
}
```