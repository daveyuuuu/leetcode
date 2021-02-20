**题目理解**

- 找到一个链表的中间节点，若为偶数长度，返回后面一个

**思考过程**

1. 设置快慢两个节点，当快节点扫描结束时，慢节点则为中间节点，见法一

**具体代码**

法一
```JavaScript
var middleNode = function(head) {
  let slow = fast = head
  while (fast && fast.next) {
    slow = slow.next
    fast = fast.next.next
  }
  return slow
}
```