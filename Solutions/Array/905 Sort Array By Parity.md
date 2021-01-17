**题目理解**

- 给定一个数组，对数组进行重排，使得偶数在前，奇数在后

**思考过程**

1. 设左右两个指针，左边遇到奇数，右边遇到偶数，就交换两者位置，见法一

**具体代码**

法一
```javascript
var sortArrayByParity = function(A) {
  let left = 0, right = A.length - 1
  while (left < right) {
    while (A[left] % 2 === 0) left++
    while (A[right] % 2 === 1) right--
    if (left < right) {
      [A[left], A[right]] = [A[right], A[left]]
    }
  }
  return A
}
```

