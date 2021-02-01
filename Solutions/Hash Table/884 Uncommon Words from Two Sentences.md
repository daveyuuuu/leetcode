**题目理解**

- 给定两个句子，都是由空格分隔的单词组成，且都为小写，找出在两个句子中只出现一次，且在两一个句子中不出现的单词

**思考过程**

1. 在两个句子中都不出现，即只出现一次，又在自己的句子中只出现一次，因此可以对所有的单词进行计数，只出现一次的皆为结果，见法一

**具体代码**

法一
```JavaScript
var uncommonFromSentences = function(A, B) {
  A = A.split(' ')
  B = B.split(' ' )
  let map = new Map()
  A.forEach(word => map.set(word, (map.get(word) || 0) + 1))
  B.forEach(word => map.set(word, (map.get(word) || 0) + 1))
  return Array(...map)
    .filter(item => item[1] === 1)
    .map(item => item[0])
}
```
