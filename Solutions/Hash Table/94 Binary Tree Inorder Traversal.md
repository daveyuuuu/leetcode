**题目理解**

- 给定一个二叉树，返回中序遍历的结果

**思考过程**

1. 递归当方式，如果空节点，返回空数组，否则，返回左子树的数组节点，再合并上当前节点与右子树的数组节点，见法一

2. 迭代方式，用栈来模拟递归的过程，分别对左右子树进行中序遍历，先不断将左子树入栈，如果左子树为空了，就弹出栈内第一个节点，记录它的值，并对它的右子树进行中序遍历，见法二

**具体代码**

法一
```javascript
var inorderTraversal = function(root) {
  if (!root) {
    return []
  }
  return inorderTraversal(root.left).concat([root.val], inorderTraversal(root.right))
}
```

法二
```javascript
var inorderTraversal = function(root) {
  const result = []
  const stack = []
  while (root || stack.length > 0) {
    if (root) {
      stack.push(root)
      root = root.left
    } else {
      root = stack.pop()
      result.push(root.val)
      root = root.right
    }
  }
  return result
}
```