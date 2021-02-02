**题目理解**

- 自己实现一个hash map

**思考过程**

1. hash map的原理是用散列函数找位置，然后用链表存储，若冲突的太多，则转为红黑树，实现过去复杂，考虑一种简单的实现，直接用key作为位置，key索引出来的值为实际元素的位置，见法一

**具体代码**

法一
```javascript
var MyHashMap = function() {
  this.index = []
  this.value = []
}

MyHashMap.prototype.put = function(key, value) {
  if (this.index[key] === undefined) {
    this.value.push(value)
    this.index[key] = this.value.length - 1
  } else {
    this.value[this.index[key]] = value
  }
}

MyHashMap.prototype.get = function(key) {
  if (this.index[key] === undefined) {
    return -1
  } else {
    return this.value[this.index[key]]
  }
}

MyHashMap.prototype.remove = function(key) {
  if (this.index[key] !== undefined) {
    this.index[key] = undefined
    this.value[this.index[key]] = undefined
  }
}
```
