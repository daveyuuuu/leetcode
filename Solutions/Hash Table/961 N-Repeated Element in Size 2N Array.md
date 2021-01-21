**题目理解**

- 给定一个长度为2n的数组，数组中有n+1个元素，元素各不相同，其中一个元素出现了n次，返回这个元素

**思考过程**

1. 因为只有一个元素出现的次数超过了1次，可以考虑用一个Set保存出现过的元素，如果有重复了则为出现N次的元素，见法一

**具体代码**

法一
```JavaScript
var repeatedNTimes = function(A) {
  let set = new Set()
  for (let n of A) {
    if (set.has(n)) {
      return n
    }
    set.add(n)
  }
}
```

