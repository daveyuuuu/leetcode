**题目理解**

- 给定一个数组candies，和一个整数extraCandies，candies的第i位代表第i个小朋友拥有的糖果，extraCandies代表额外的糖果
- 求解任何一个小朋友拿到额外的糖果之后是否成为拥有最多糖果的小朋友

**思考过程**

1. 判断是否为糖果最多的，即判断下式是否成立$candies[i] + extraCandies >= candies(0\backsim n)$

2. 因为要大于$0\backsim n$ 的任一个，所以只需和最大的比较即可，见法一

3. JS风格的做法,one line，见法二

4. 应该把Math.max(...candies)提取出来，避免重复计算，见注释

**具体代码**

法一
```javascript
var kidsWithCandies = function(candies, extraCandies) {
    const max = Math.max(...candies)
    const result = []
    for (const val of candies) {
      if ((val + extraCandies) >= max) {
        result.push(true)
      } else {
        result.push(false)
      }
    }
    return result
}
```

法二
```javascript
var kidsWithCandies = function(candies, extraCandies) {
    return candies.map(val => (val + extraCandies) >= Math.max(...candies))
    
    // const max = Math.max(...candies)
    // return candies.map(val => (val + extraCandies) >= max)
}
```