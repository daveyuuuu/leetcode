**题目理解**

- 给定一个数组，除了其中一个元素，其他元素全部出现2次，找到那个出现一次的元素

**思考过程**

1. 用一个Set保存，遍历过程中的每个元素，若出现过，就删去，最后只剩下出现一次的元素，见法一

2. 一个数字和自己异或的结果为0，对所有的元素进行异或操作，最后结果即为出现一次的元素，见法二


**具体代码**

法一
```javascript
var singleNumber = function(nums) {
  let set = new Set()
  nums.forEach(num => {
    if (set.has(num)) {
      set.delete(num)
      return
    }
    set.add(num)
  })
  return [...set][0]
}
```

法二
```javascript
var singleNumber = function(nums) {
  let result = 0
  nums.forEach(num => result ^= num)
  return result
}
```