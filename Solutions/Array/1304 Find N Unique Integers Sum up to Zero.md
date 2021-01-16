**题目理解**

- 给定一个数组n，返回一个长度为n的数组，数组中的元素之和为0，且数组中的元素不得重复

**思考过程**

1. 每次添加一个正数和一个负数，因此要考虑奇数和偶数两种情况，奇数在在添加一个0，见法一

2. 或者一直加n-1个数，最后一个放前n个数和的相反数，见法二

**具体代码**

法一
```javascript
var sumZero = function(n) {
  let odd = false
  if (n % 2 === 1) {
    odd = true
  }
  const result = []
  for (let i = 1; i <= Math.floor(n/2); ++i) {
    result.push(i)
    result.push(-i)
  }
  if (odd) {
    result.push(0)
  }
  return result
}
```

法二
```javascript
var sumZero = function(n) {
  const result = []
  let sum = 0
  for (let i = 0; i < n-1; ++i) {
    result.push(i)
    sum += i
  }
  result.push(-sum)
  return result
}
```
