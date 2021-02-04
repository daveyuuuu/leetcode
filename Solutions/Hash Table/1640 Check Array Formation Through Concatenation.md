**题目理解**

- 给定一个一维数组和一个二维数组，判断二维数组中的一维数组的组合是否可以组成一维数组

**思考过程**

1. 将目标数组转为字符串来比较，用map存储二维数组中的数组，因为数组必须全部使用，可以用第一个值作为键，然后进行重组，见法一

**具体代码**

法一
```JavaScript
var canFormArray = function(arr, pieces) {
  let str = arr.join('')
  let map = {}
  pieces.forEach(piece => {
    map[piece[0]] = piece
  })
  let result = ''
  arr.forEach(num => {
    if (map[num] !== undefined) {
      result += map[num].join('')
    }
  })
  return result === str
}
```