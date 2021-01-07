**题目理解**

- 给定一个只包含正数的数组，计算所有个数为奇数的子数组的元素之和，这里的子数组必须是连续的，返回总和

**思考过程**

1. 最直接的思路就是按照题意，先找到所有的奇数子数组，然后求和，见法一

2. 法一$O(n^3)$复杂度太高，考虑对其进行优化，对数组中的第i个元素，i左边有(i+1)个元素选择（包括i），i右边有(n-i)个元素选择，一共有(i+1)\*(n-i)中选择，其中合起来数组长度为奇数的选择有((i+1)\*(n-i)+1)/2中选择，即该数字在所有奇数长度数组中出现的次数，见法二

**具体代码**

法一
```JavaScript
var sumOddLengthSubarrays = function(arr) {
    let result = 0
    for (let i = 1; i <= arr.length; i += 2) {
      for (let j = 0 ; j < arr.length; ++j) {
        for (let k = j; k < j + i && k < arr.length && j + i <= arr.length; ++k) {
          result += arr[k]
        }
      }
    }
    return result
}
```

法二
```JavaScript
var sumOddLengthSubarrays = function(arr) {
  let result = 0
  for (let i = 0; i < arr.length; ++i) {
    result += Math.floor(((i+1)*(arr.length-i)+1)/2) * arr[i]
  }
  return result
}
```
