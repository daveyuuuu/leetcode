**题目理解**

- 计算数组中偶数位数的元素的个数

**思考过程**

1. 常见思路就是用除法或转为字符串求位数，现在记录评论区见到的巧妙的方法，主要在于题目的大小限制，见法一

**具体代码**

法一
```JavaScript
var findNumbers = function(nums) {
    let result = 0
    for (const val of nums) {
      if (
        (val >= 10 && val <= 99) ||
        (val >= 1000 && val <= 9999) ||
        (val === 100000)
         ) {
          result += 1
        }
    }
    return result
}
```

