**题目理解**

- 给定一个链表，链表表示的是一个数的二进制形式，还原这个数

**思考过程**

1. 可以先转为字符串，然后再进行转换，见法一

2. 直接一边遍历一边还原，用左移操作进行还原，见法二

**具体代码**

法一
```JavaScript
var getDecimalValue = function(head) {
    let result = ''
    while (head !== null) {
        result += head.val
        head = head.next
    }
    return Number.parseInt(result, 2)
    111
    101
}
```

法二
```JavaScript
var getDecimalValue = function(head) {
  let result = 0
  while (head !== null) {
    result <<= 1
    result |= head.val
    head = head.next
  }
  return result
}
```

