**题目理解**

- 给定一个字符串，求出字符串中所有字符能够组成‘balloon'的个数

**思考过程**

- 记录字符串中所有字符出现的次数，找到需要组成balloon的最少的源字符，每个balloon需要1a,1b,2l,2o,1n，用总数分别处以1/1/2/2/1，最小的即是可以组成的数目，见法一

**具体代码**

法一
```JavaScript
var maxNumberOfBalloons = function(text) {
  let map = new Map()
  for (let ch of text) {
    map.set(ch, (map.get(ch) || 0) + 1)
  }
  const obj = {
    'b': 1,
    'a': 1,
    'l': 2,
    'o': 2,
    'n': 1,
  }
  let result = Infinity
  for (let ch in obj) {
    if (map.get(ch) === undefined) {
      result = 0
      break
    }
    const n = map.get(ch)
    result = Math.min(result, Math.floor(n / obj[ch]))
  }
  return result
}
```

