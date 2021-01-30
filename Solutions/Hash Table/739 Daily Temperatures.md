**题目理解**

- 给定一个每日温度的数组，对于每一天的温度，计算离下一个更温暖的日子的天数，如[73, 74, 75, 71, 69, 72, 76, 73]，对应的输出应该为[1, 1, 4, 2, 1, 1, 0, 0]

**思考过程**

1. 即求下一个比当前位置大的数字的距离，简单粗暴的方法就是双重循环直接寻找，见法一

2. 因为数字的范围是30~100，当遍历数组中每一天的温度时，在遍历当前温度~100，看是否存在比它大的温度，即哈希的思想，用数字当键，位置作为值，见法二

3. 针对法二的优化，可以一边遍历，一边求值，且从后往前遍历，减少计算量， 见法三

4. 用栈来存储温度的位置，如果遇到比栈顶元素小的元素，直接push进去，否则弹出栈顶元素并计算相隔的天数，见法四

**具体代码**

法一
```javascript
var dailyTemperatures = function(T) {
  const result = []
  for (let i = 0; i < T.length; ++i) {
    let distance = 1
    // 标志位，判断是否存在比当前位置大的数字
    let flag = false
    for (let j = i + 1; j < T.length; ++j) {
      if (T[j] > T[i]) {
        result.push(distance)
        flag = true
        break
      } else {
        distance++
      }
    }
    if (!flag) {
      result.push(0)
    }
  }
  return result
}
```

法二
```javascript
var dailyTemperatures = function(T) {
  let map = new Map()
  for (let i = 0; i < T.length; ++i) {
    if (!map.get(T[i])) {
      map.set(T[i], [i])
    } else {
      map.get(T[i]).push(i)
    }
  }
  const result = []
  for (let i = 0; i < T.length; ++i) {
    let min = Infinity
    for (let j = T[i]+1; j <= 100; ++j) {
      if (map.get(j) !== undefined) {
        let temp = map.get(j)
        for (let k = 0; k < temp.length; ++k) {
          if (temp[k] > i) {
            min = Math.min(temp[k]-i, min)
          }
        }
      }
    }
    if (min === Infinity) {
      result.push(0)
    } else {
      result.push(min)
    }
  }
  return result.reverse()
}
```

法三
```javascript
var dailyTemperatures = function(T) {
  let map = new Map()
  const result = []
  for (let i = T.length-1; i >= 0; --i) {
    if (map.get(T[i]) === undefined) {
      map.set(T[i], [i])
    } else {
      map.get(T[i]).push(i)
    }
    let min = Infinity
    for (let j = T[i] + 1; j <= 100; ++j) {
      if (map.get(j) !== undefined) {
        let temp = map.get(j)
        for (let k = 0; k < temp.length; ++k) {
          min = Math.min(min, temp[k] - i)
        }
      }
    }

    if (min === Infinity) {
      result.push(0)
    } else {
      result.push(min)
    }
  }
  return result
}
```

法四
```javascript
var dailyTemperatures = function(T) {
  let stack = []
  let result = new Array(T.length).fill(0)
  for (let i = 0; i < T.length; ++i) {
    while (stack.length > 0 && T[i] > T[stack[stack.length-1]]) {
      let pre = stack.pop()
      result[pre] = i - pre
    }
    stack.push(i)
  }
  return result
}
```