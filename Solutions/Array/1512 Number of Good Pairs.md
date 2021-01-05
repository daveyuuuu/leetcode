**题目理解**

- 给定一个整数数组，对于数组中的两个元素，如果两个元素相等，即为good，返回这样的匹配数，换句话说就是找数组中相同元素的对数，一个元素可以多次使用

**思考过程**

1. 记录不同元素出现的次数，然后从出现的次数-1加到1（第一个可以和剩下的n-1匹配，第二个可以和剩下的n-2匹配...），求每个不同元素的匹配数，最后求和，见法一

2. 并不需要全部记录下来在逐个遍历计算，可以一边遍历，一边计算，即当前出现的元素可以和之前出现的若干个元素进行匹配，见法二

**具体代码**

法一
```javascript
var numIdenticalPairs = function(nums) {
  function calc (n) {
    let sum = 0
    for (let i = n-1; i >= 1; --i) {
      sum += i
    }
    return sum
  }
  const count = {}
  for (const n of nums) {
    count[n] = count[n] + 1 || 1
  }
  let result = 0
  for (const key in count ) {
    if (count.hasOwnProperty(key)) {
      if (count[key] >= 2) {
        result += calc(count[key])
      }
    }
  }
  return result
}
```

法二
```javascript
var numIdenticalPairs = function(nums) {
  let result = 0
  const count = {}
  for (const val of nums) {
    if (!count[val]) {
      count[val] = 1
    } else {
      result += count[val]
      count[val] += 1
    }
  }
  return result
}
```