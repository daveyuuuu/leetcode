**题目理解**

- 给定一个数组，求其中递增或递减的长度为3的子数组的个数（可以不连续）

**思考过程**

1. 用三重循环对所有情况进行穷举，见法一

2. 因为子数组长度为3，所以只需对子数组中间的元素进行考虑，只有两种情况，$a<b<c$或$a>b>c$，因此计算数组元素左边比它小的元素和右边比它大的元素的个数，和左边比它大的元素和右边比它小的元素的个数，这两种情况的左右任意搭配，见法二

**具体代码**

法一
```JavaScript
var numTeams = function(rating) {
    let result = 0
    for (let i = 0; i < rating.length; ++i) {
      for (let j = i + 1; j < rating.length; ++j) {
        for (let k = j + 1; k < rating.length; ++k) {
          if (
            (rating[i] > rating[j] && rating[j] > rating[k]) ||
            (rating[i] < rating[j] && rating[j] < rating[k])) {
              result += 1
          }
        }
      }
    }
    return result
}
```

法二
```JavaScript
var numTeams = function(rating) {
  const leftLess = new Array(rating.length).fill(0)
  const rightLess = new Array(rating.length).fill(0)
  const leftMore = new Array(rating.length).fill(0)
  const rightMore = new Array(rating.length).fill(0)

  let result = 0
  
  for (let i = 1; i < rating.length - 1; ++i) {
    let leftLessTemp = 0
    let leftMoreTemp = 0
    for (let j = 0; j < i; ++j) {
      if (rating[j] < rating[i]) {
        leftLessTemp += 1
      } else {
        leftMoreTemp += 1
      }
    }
    leftLess[i] = leftLessTemp
    leftMore[i] = leftMoreTemp

    let rightLessTemp = 0
    let rightMoreTemp = 0
    for (let j = i + 1; j < rating.length; ++j) {
      if (rating[j] > rating[i]) {
        rightMoreTemp += 1
      } else {
        rightLessTemp += 1
      }
    }
    rightMore[i] = rightMoreTemp
    rightLess[i] = rightLessTemp
  }
  for (let i = 1; i < rating.length; ++i) {
    result += leftLess[i] * rightMore[i] + leftMore[i] * rightLess[i]
  }
  return result
}
```
