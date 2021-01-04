**题目理解**

- 给定一个数组，结果返回一个新数组，新数组的定义如下为，第i位元素等于0-i位元素之和

**思考过程**

1. 遍历数组，用一个临时变量储存对0-i位的求和，将每一次求和的结果加入新的结果数组，见法一
2. 题目并没有要求返回新数组，因此考虑in-place的方法，对i位左边的元素进行累加并替换原有值，从而优化空间复杂度，见法二
3. 其实，法二也可以理解为动态规划，只不过dp数组直接初始化为nums数组

$$
dp(i)= \begin{cases} nums[i], & i = 0 \\ dp[i-1]+nums[i], & i>=1 \end{cases}
$$

4. JS风格的做法，见法三

**具体代码**

法一：
```javascript
var runningSum = function(nums) {
  let temp = 0
  const result = []
  for (const n of nums) {
    temp += n
    result.push(temp)
  }
  return result
}
```

法二：
```javascript
var runningSum = function(nums) {
  for (let i = 1; i < nums.length; ++i) {
    nums[i] += nums[i-1]
  }
  return nums
}
```

法三：
```javascript
var runningSum = function(nums) {
  /*
   * reduce，接受两个参数
   * 第一个参数为回调函数，该回调函数接受4个参数
   * acc 累加值
   * cur 当前值
   * ind 当前索引
   * src 源数组
   * 第二个参数为acc的初始值
   * 若不传入，则默认为数组的第一个元素
   */
  nums.reduce((acc, cur, ind, nums) => nums[ind] += acc, 0)
  return nums
}
```