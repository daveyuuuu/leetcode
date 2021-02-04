**题目理解**

- 实现一个栈，一个入栈函数和一个出栈函数，出栈函数要求弹出出现次数最多的元素，如果由多个，返回靠近栈顶的那个元素

**思考过程**

1. 因为要弹出出现次数最多的元素，所以肯定要一个map进行计数，再维护一个数组作为栈，将出现次数相同的元素放在一起，见法一

**具体代码**

```javascript
var FreqStack = function() {
  this.stack = []
  this.map = {}
}
FreqStack.prototype.push = function(x) {
  this.map[x] = this.map[x] ? this.map[x] + 1 : 1
  if (this.stack.length < this.map[x]) {
    this.stack.push([x])
  } else {
    // 转为数组索引， 所以需减一
    this.stack[this.map[x] - 1].push(x)
  }
}
FreqStack.prototype.pop = function() {
  const top = this.stack[this.stack.length - 1]
  const result = top.pop()
  if (top.length === 0) {
    this.stack.pop()
  }
  this.map[result] -= 1
  return result
}
```
