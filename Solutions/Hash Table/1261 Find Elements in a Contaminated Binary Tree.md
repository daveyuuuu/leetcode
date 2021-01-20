**题目理解**

- 给定一个值全为-1的二叉树，让你对其按指定规则进行，还原，并判断是否包含指定元素

**思考过程**

1. 因为并没有要求返回复原的二叉树，可以保存所有复原的值，用Set保存，避免重复，遍历可以考虑深度优先搜索，见法一

**具体代码**

法一
```JavaScript
var FindElements = function(root) {
  this.vals = new Set()
  let dfs = (root, val) => {
    if (root) {
      this.vals.add(val)
      dfs(root.left, 2 * val + 1)
      dfs(root.right, 2 * val + 2)
    }
  }
  dfs(root, 0)
}

FindElements.prototype.find = function(target) {
  return this.vals.has(target)
}
```
