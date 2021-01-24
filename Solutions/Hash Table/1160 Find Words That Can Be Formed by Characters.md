**题目理解**

- 给定一个单词数组和一个字符串，返回数组中所有能够被字符串拼出来的单词的长度，全为小写

**思考过程**

1. 记录字符串中所有单词出现的次数，对单词进行遍历，遍历时，用字符串中单词出现的次数减去当前单词中字符出现的次数，如果小于0，说明不能拼成，否则加上当前单词的长度，见法一

2. 用字符串中的每一个字符去替换单词，若单词能够被替换成空字符串，说明能够拼成，见法二

**具体代码**

法一
```javascript
var countCharacters = function(words, chars) {
  let count = new Array(26).fill(0)
  let result = 0

  for (let i = 0; i < chars.length; ++i) {
    count[chars[i].charCodeAt()-97]++
  }

  words.forEach(word => {
    let temp = [...count]
    let flag = false
    for (let i = 0; i < word.length; ++i) {
      temp[word[i].charCodeAt()-97]--
      if (temp[word[i].charCodeAt()-97] < 0) {
        flag = true
        break
      } 
    }
    if (!flag) {
      result += word.length
    }
  })
  return result
}
```

法二
```javascript
var countCharacters = function(words, chars) {
  return words.reduce((acc, word, ind) => {
    for (const c of chars) {
      word = word.replace(c, '')
    }
    return acc + (word.length === 0 ? words[ind].length : 0)
  }, 0)
}
```

