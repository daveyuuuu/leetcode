**题目理解**

- 给定一个牌堆，对牌堆的顺序进行重排，使得按指定的规则拿出的牌是有序的

**思考过程**

1. 要拿出有序的牌堆，可以先将牌堆排序然后按逆向的规则放回，即为重排后的结果，见法一，逆向规则如下

    1.1 将牌底的牌置于牌顶（如果没牌，先拿牌）
    1.2 拿一张牌放入牌顶

**具体代码**

法一
```javascript
var deckRevealedIncreasing = function(deck) {
    deck.sort((a,b)=>b-a)
    const result = []
    while (deck.length > 0) {
      if (result.length == 0) {
        result.push(deck.shift())
      }
      if (deck.length > 0) {
        result.unshift(result.pop())
        result.unshift(deck.shift())
      }
    }
    return result
}
```

