**题目理解**

- 给定一个数组（每个元素要么是0，要么是1），要求先水平翻转数组，然后在对每个元素进行反转（0->1，1->0），返回最后的结果

**思考过程**

1. 按照题目进行操作，先水平翻转，即对数组的每一行头尾进行交换，直到中间元素的位置，同时可以进行反转的操作，见法一

2. JS风格的做法，见法二

**具体代码**

法一
```javascript
var flipAndInvertImage = function(A) {
  for (let i = 0; i < A.length; ++i) {
    let j = 0, k = A[i].length - 1
    while (j <= k) {
      // 对奇数个数的中间元素处理
      if (j === k) {
        A[i][j] ^= 1
        break
      } else if (j > k ) {
        break
      } else {
        [A[i][j], A[i][k]] = [A[i][k], A[i][j]];
        A[i][j] ^= 1
        A[i][k] ^= 1
      }
      j++
      k--
    }
  }
  return A
}
```

法二
```javascript
var flipAndInvertImage = function(A) {
  return A.map(row => row.reverse().map(col => col ^= 1))
}
```

