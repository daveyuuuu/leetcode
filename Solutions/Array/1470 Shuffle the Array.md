**题目理解**

- 给定一个参数n，一个数组[x1,x2,...,xn,y1,y2,...,yn],以[x1,y1,x2,y2,...,xn,yn]形式返回

**思考过程**

1. 因为数组包含2n个元素，所以数组中第n个即为y1，对数组开头和中间部位进行遍历，每一轮循环将x,y分别放入数组，见法一

2. 考虑in-place的方法，优化空间复杂度

    1. 由题目的规律可知，对于数组的前n位元素，它最终的位置应该是i*n，对于后n位元素，它最终的位置应该是(i-n)*2+1

    2. 遍历数组中的每一个元素，并求它的最终位置，用j表示，将当前元素放入它的最终位置j,并置为相反数，表示改元素已在最终位置，将j位置的元素放入当前元素的位置，即交换j和i位置的元素，并将当前元素取负，接着判断当前位置是否存放的为最终元素

    3. 如果是，则进入下一轮循环；如果不是，则递归的去找j位置元素的最终位置，直到当前位置存放的是最终元素

    4. 最后对所有元素取反，即最终结果

3. 位运算的方法，[详情点此链接](https://leetcode.com/problems/shuffle-the-array/discuss/675956/In-Place-O(n)-Time-O(1)-Space-With-Explanation-and-Analysis)，见法三

**具体代码**

法一
```javascript
var shuffle = function(nums, n) {
    const result = []
    for (let i = 0, j = n; i < n; ++i, ++j) {
      result.push(nums[i])
      result.push(nums[j])
    }
    return result
}
```

法二
```javascript
var shuffle = function(nums, n) {
  function getInd(i) {
    return i < n ? 2 * i : (i - n) * 2 + 1
  }
  for (let i = 0; i < 2 * n; ++i) {
    let j = i
    while (nums[i] > 0) {
      j = getInd(j);
      // 注意交换顺序，本质上还是数组的解构赋值
      [nums[i], nums[j]] = [nums[j], -nums[i]];
    }
  }
  for (let i = 0; i < 2 * n; ++i) {
    nums[i] = -nums[i]
  }
  return nums
}
```

法三
```javascript
var shuffle = function(nums, n) {
  let i = 0
  for (let j = n; j < 2 * n; ++j) {
    nums[j] <<= 10
    nums[j] |= nums[i++]
  }
  i = 0
  for (let j = n; j < 2 * n; ++j) {
    const nums1 = nums[j] & 1023
    const nums2 = nums[j] >> 10
    nums[i] = nums1
    nums[i+1] = nums2
    i += 2
  }
  return nums
}
```
