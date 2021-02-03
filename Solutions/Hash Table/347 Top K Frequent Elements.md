**题目理解**

- 给定一个数组和一个数字k，返数组中回k个出现最频繁的数字

**思考过程**

1. 对数组中的元素进行计数，然后按出现的次数进行排序，取前k个，见法一

2. 可以采用桶排序的思想，将出现次数一样的数字放在一起，见法二

**具体代码**

法一
```javascript
var topKFrequent = function(nums, k) {
  let map = new Map()
  for (let n of nums) {
    map.set(n, (map.get(n) || 0) + 1)
  }
  let sorted = Array(...map).sort((a,b) => b[1] - a[1])
  let result = []
  for (let _ = 0; _ < k; ++_) {
    result.push(sorted[_][0])
  }
  return result
}
```

法二
```javascript
var topKFrequent = function(nums, k) {
  let map = new Map()
  for (let n of nums) {
    map.set(n, (map.get(n) || 0) + 1)
  }
  let sorted = []
  for (let [val, freq] of map) {
    sorted[freq] = (sorted[freq] || new Set()).add(val)
  }
  const result = []
  for (let _ = sorted.length - 1; _ >= 0; --_) {
    if (sorted[_]) {
      result.push(...sorted[_])
    }
    if (result.length === k) {
      break
    }
  }
  return result
}
```