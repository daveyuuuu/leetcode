**题目理解**

- 自己实现一个哈希表

**思考过程**

1. 用一个二维的数组来存取，一维通过哈希函数来计算（素数去模），二维线性增减，见法一

**具体代码**

法一
```javascript
var MyHashSet = function() {
  this.PRIME = 7793
  // ES6
  // 结构赋值会遍历EMPTY
  // this.hash = [...Array(this.PRIME)].map(_ => [])
  this.hash = new Array(this.PRIME).fill(undefined).map(_ => [])
}

MyHashSet.prototype.add = function(key) {
  const ind = key % this.PRIME
  this.hash[ind].push(key)
}

MyHashSet.prototype.remove = function(key) {
  const ind = key % this.PRIME
  this.hash[ind] = this.hash[ind].filter(item => item !== key)
}

MyHashSet.prototype.contains = function(key) {
  const ind = key % this.PRIME
  return this.hash[ind].indexOf(key) > -1 ? true: false
}
```
