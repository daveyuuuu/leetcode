**题目理解**

给定一个数组，返回数组中最大两个元素减一的乘积

**思考过程**

1. 双重循环进行遍历，记录最大值，见法一

2. 其实只要找到最大的两个元素即可，可以先排序，见法二

3. 考虑到只需要找最大的两个数，因此可以直接遍历并记录，即topk问题，见法三

**具体代码**

法一
```javascript
var maxProduct = function(nums) {
  let result = 0
  for (let i = 0; i < nums.length; ++i) {
    for (let j = i + 1; j < nums.length; ++j) {
      result = Math.max(result, (nums[i]-1)*(nums[j]-1))
    }
  }
  return result
}
```

法二
```javascript
var maxProduct = function(nums) {
  nums.sort((a,b)=>b-a)
  return (nums[0]-1)*(nums[1]-1)
}
```

法三
```javascript
var maxProduct = function(nums) {
  let first = nums[0] > nums[1] ? nums[0] : nums[1]
  let second = nums[1] < nums[0] ? nums[1] : nums[0]

  for (let i = 2; i < nums.length; ++i) {
    if (nums[i] > first) {
      second = first
      first = nums[i]
    } else if (nums[i] > second) {
      second = nums[i]
    } else {
      continue
    }
  }
  return (first-1) * (second-1)
}
```
