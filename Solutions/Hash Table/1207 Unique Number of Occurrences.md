**题目理解**

- 给定一个数组，如果数组中每个元素出现的次数都是唯一的就返回true

**思考过程**

1. 用一个hash存储每个元素出现的次数，最后在遍历出现的次数，看是否有重复，见法一

2. 因为数组的元素范围为-1000~1000，可以考虑用一个长度为2001的数组来保存每个元素出现的次数，负数就加1000，然后进行排序，若左右有相邻的一样的元素，说明出现的次数一样，见法二

**具体代码**

法一
```JavaScript
var uniqueOccurrences = function(arr) {
  let map = new Map()
  for (let n of arr) {
    if (map.get(n) === undefined) {
      map.set(n, 1)
    } else {
      map.set(n, map.get(n) + 1)
    }
  }
  let set = new Set()
  for (let val of map.values()) {
    if (set.has(val)) {
      return false
    }
    set.add(val)
  }
  return true
}
```

法二
```JavaScript
var uniqueOccurrences = function(arr) {
  const count = new Array(2001).fill(0)
  for (let n of arr) {
    count[n+1000]++
  }
  count.sort()
  for (let i = 1; i < count.length; ++i) {
    if (count[i] !== 0 && count[i] === count[i-1]) {
      return false
    }
  }
  return true
}
```
