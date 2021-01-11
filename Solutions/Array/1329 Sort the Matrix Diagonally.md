**题目理解**

- 给定一个数组，对它的对角线（左上->右下）进行排序（看题目图片比较容易理解，不赘述），返回排序之后的数组。

**思考过程**

1. 遍历每一个对角线，将数据储存之后在进行排序，用排序后的结果替换原结果，关键是如何储存每一个对角线，注意到同一个对角线的$i-j$的值是一样的，所以可以用map来进行保存，见法一

**具体代码**

法一
```javascript
var diagonalSort = function(mat) {
  const map = new Map()
  for (let i = 0; i < mat.length; ++i) {
    for (let j = 0; j < mat[0].length; ++j) {
      let ind = i - j
      if (map.get(ind) === undefined) {
        map.set(ind, [])
      }
      map.get(ind).push(mat[i][j])
    }
  }
  for (var [key, value] of map) {
    value.sort((a,b)=>a-b)
  }
  for (let i = 0; i < mat.length; ++i) {
    for (let j = 0; j < mat[0].length; ++j) {
      let ind = i - j
      mat[i][j] = map.get(ind).shift()
    }
  }
  return mat
}
```

