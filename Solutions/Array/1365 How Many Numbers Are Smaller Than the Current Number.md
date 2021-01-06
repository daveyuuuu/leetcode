**题目理解**

- 给定一个数组，对于数组中的每个元素，找出比它小的元素的个数，并记录在新数组的对应位置，返回这个新数组

**思考过程**

1. 最直接的思路，用一个双重循环，跳过与自己的比较，遇到比它小的数字，则加一，见法一

2. 法一的复杂度显然太高，换种思路，先对数组进行排序，然后根据排序后的位置即知道比它小的元素有几个，见法二

3. 考虑到数字范围属于$0\leq nums[i] \leq 100$，考虑用一个数组对所有元素计数，比n小的数即为0~n-1的数字出现的次数，见法三

**具体代码**

法一
```JavaScript
var smallerNumbersThanCurrent = function(nums) {
    const result = []
    for (let i = 0; i < nums.length; ++i) {
      let temp = 0
      for (let j = 0; j < nums.length; ++j) {
        if (i !== j && nums[j] < nums[i]) {
          temp += 1
        }
      }
      result.push(temp)
    }
    return result
}
```

法二
```JavaScript
var smallerNumbersThanCurrent = function(nums) {
  let sorted = Array.from(nums).sort((a,b) => a-b)
  let numToIndex = {}
  for (let i = 0; i < sorted.length; ++i) {
    if (numToIndex[sorted[i]] === undefined) {
      numToIndex[sorted[i]] = i
    }
  }
  for (let i = 0; i < nums.length; ++i) {
    sorted[i] = numToIndex[nums[i]]
  }
  return sorted
}
```

法三
```JavaScript
var smallerNumbersThanCurrent = function(nums) {
  let count = new Array(101).fill(0)
  for (const val of nums) {
    count[val] += 1
  }
  for (let i = 1; i < count.length; ++i) {
    count[i] += count[i-1]
  }
  const result = []
  for (const val of nums) {
    result.push(val >= 1 ? count[val-1] : 0)
  }
  return result
}
```
