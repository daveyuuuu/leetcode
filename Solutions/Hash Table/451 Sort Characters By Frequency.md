**题目理解**

- 给定一个字符串，对字符进行重新排序，顺序为字符串中字符出现的次数降序

**思考过程**

1. 分别统计所有字符出现的次数，然后对次数进行排序，见法一

2. 在统计完之后，可以不必进行排序，因为出现的次数最多为字符串的长度，所以可以将频次相同的字符放在一起，见法二

**具体代码**

法一
```JavaScript
var frequencySort = function(s) {
  let map = new Map()
  for (let ch of s) {
    if (!map.get(ch)) {
      map.set(ch,1)
    } else {
      map.set(ch, map.get(ch)+1)
    }
  }
  let arr = new Array(...map)
  arr.sort((a,b) => b[1] - a[1])
  let result = ''
  for (let [ch, n] of arr) {
    for (let _ = 0; _ < n; ++_) {
      result += ch
    }
  }
  return result
}
```

法二
```JavaScript
var frequencySort = function(s) {
  let map = new Map()
  for (let ch of s) {
    if (!map.get(ch)) {
      map.set(ch,1)
    } else {
      map.set(ch, map.get(ch)+1)
    }
  }
  let arr = new Array(s.length)
  for (let [ch, freq] of map) {
    if (!arr[freq]) {
      arr[freq] = new Array()
    }
    arr[freq].push(ch.repeat(freq))
  }
  let result = ''
  for (let i = arr.length - 1; i >= 1; --i) {
    if (arr[i]) {
      arr[i].forEach(str => result += str)
    }
  }
  return result
}
```