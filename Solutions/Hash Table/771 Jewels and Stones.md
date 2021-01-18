**题目理解**

- 给定两个字符串，jewels代表的是珠宝，stones代表你手里的石头，让你根据jewels判断自己手里有多少个珠宝

**思考过程**

1. 对手里的每一个石头进行遍历，在对珠宝进行遍历，看当前的石头是否为珠宝，见法一

2. 因为至少要遍历自己手上的所有石头，所以外层循环无法优化，可以考虑将珠宝的字符串做成一个哈希表，为了避免重复，用set进行存储，见法二

**具体代码**

法一
```JavaScript
var numJewelsInStones = function(jewels, stones) {
  let result = 0
  for (let i = 0;i < stones.length; ++i) {
    for (let j = 0; j < jewels.length; ++j) {
      if (stones[i] === jewels[j]) {
        result++
      }
    }
  }
  return result
}
```

法二
```JavaScript
var numJewelsInStones = function(jewels, stones) {
  let hash = new Set()
  for (let i = 0; i < jewels.length; ++i) {
    hash.add(jewels[i])
  }
  let result = 0
  for (let i = 0; i < stones.length; ++i) {
    if (hash.has(stones[i])) {
      result++
    }
  }
  return result
}
```
