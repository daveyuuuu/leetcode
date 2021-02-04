**题目理解**

- 给定一个字符串数组，将所有的易位构词放在一起

**思考过程**

1. 将排序之后的单词作为键，再进行存储，见法一

**具体代码**

法一
```JavaScript
var groupAnagrams = function(strs) {
  let map = {}
  strs.forEach(str => {
    const key = str.split('').sort().join('')
    if (!map[key]) {
      map[key] = []
    }
    map[key].push(str)
  })
  const result = []
  for (let key in map) {
    result.push(map[key])
  }
  return result
}
```
