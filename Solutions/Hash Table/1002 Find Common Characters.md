**题目理解**

- 给定一个全是小写字母的字符串数组，求出现在所有字符串中的字符，可以是重复的

**思考过程**

1. 对每一个字符串中的字母进行计数，留下出现较少次数的结果，见法一

2. 直接将第一个字符串的所有字符当作结果，对后续的字符串进行对比，如果没有出现就过滤掉当前字符串，见法二

**具体代码**

法一
```javascript
var commonChars = function(A) {
  let count = new Array(26).fill(0)
  let first = A[0]
  for (let i = 0; i < first.length; ++i) {
    count[first[i].charCodeAt() - 'a'.charCodeAt()]++
  }

  for (let i = 1; i < A.length; ++i) {
    const str = A[i]
    let newCount = new Array(26).fill(0)
    for (let j = 0; j < str.length; ++j) {
      newCount[str[j].charCodeAt() - 'a'.charCodeAt()]++
    }
    for (let j = 0; j < 26; ++j) {
      count[j] = Math.min(count[j], newCount[j])
    }
  }

  const result = []
  for (let i = 0; i < 26; ++i) {
    if (count[i] > 0) {
      for (let j = 0; j < count[i]; ++j) {
        result.push(String.fromCharCode(i+97))
      }
    }
  }
  return result
}
```

法二
```javascript
var commonChars = function(A) {
  // ES6 将字符串转数组的快捷方式
  let result = [...A[0]]
  for (let i = 1; i < A.length; ++i) {
    result = result.filter(c => {
      let len = A[i].length
      A[i] = A[i].replace(c, '')
      return len >A[i].length
    })
  }
  return result
}
```

