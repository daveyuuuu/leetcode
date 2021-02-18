**题目理解**

- 给定两个链表，和两个数字a和b，分别代表第一个链表中的第a个位置和第b个位置，将a-b删除并替换为第二个链表

**思考过程**

1. 找到a前面的位置、b后面的位置和第二个链表的最后一个节点，然后进行链接即可，见法一

**具体代码**

```JavaScript
var mergeInBetween = function(list1, a, b, list2) {
  let cur = list1
  let pre = cur
  let count = 0
  while (count !== a) {
    pre = cur
    cur = cur.next
    count++
  }
  while (count !== (b+1)) {
    let temp = cur
    cur = cur.next
    delete temp
    count++
  }
  let tail = list2
  while (tail.next !== null) {
    tail = tail.next
  }
  pre.next = list2
  tail.next = cur
  return list1
}
```
