**题目理解**

- 给定一个0-1数组，翻转若干列，使得最多的行为全0或全1，求最多有几行？

**思考过程**

1. 从结果分析，假设若干次反转后，i,j行为全0，k行为全1，则反转之前，i和j必须一致，i，j和k则为完全相反，见法一

2. 在法一的基础上，要么找到一样的，要么找到完全相反的，即找到一种模式来代表相同形式，因为只有0和1，可以用0表示翻转或未翻转，或者用1，记录所有的形式，找到出现次数最多的即可，见法二

**具体代码**

法一
```JavaScript
var maxEqualRowsAfterFlips = function(matrix) {
  let result = 1
  for (let i = 0; i < matrix.length; ++i) {
    let flip = []
    for (let j = 0; j < matrix[i].length; ++j) {
      flip.push(1-matrix[i][j])
    }
    let count = 1
    for (let j = i+1; j < matrix.length; ++j) {
      if (JSON.stringify(matrix[j]) === JSON.stringify(matrix[i]) || 
      JSON.stringify(matrix[j]) === JSON.stringify(flip)) {
        count += 1
      }
    }
    result = Math.max(result, count)
  }
  return result
}
```

法二
```JavaScript
var maxEqualRowsAfterFlips = function(matrix) {
  let map = {}
  let result = 0
  matrix.forEach(row => {
    let one = two = ''
    row.forEach(val => {
      one += val === 0 ? 'c' : 's'
      two += val === 0 ? 's' : 'c'
    })
    map[one] = (map[one] || 0) + 1
    map[two] = (map[two] || 0) + 1
    result = Math.max(result, map[one], map[two])
  })
  return result
}
```


