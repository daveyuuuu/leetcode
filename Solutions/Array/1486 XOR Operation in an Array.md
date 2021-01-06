**题目理解**

- 给定一个整数n和一个整数start，定义一个长度为n的数组，数组的第i个元素$nums[i]=start+2*i$，返回所有数组元素的异或操作的结果

**思考过程**

1. 按照题目意思进行编码，见法一

**具体代码**
法一
```javascript
var xorOperation = function(n, start) {
    let result = start
    for (let i = 1; i < n; ++i) {
      result ^= 2 * i + start
    }
    return result
}
```

