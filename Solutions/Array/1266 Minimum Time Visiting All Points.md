**题目理解**

- 给定一个数组中，数组中有连续的若干个坐标($x_1,x_2$)，现在要桉顺序访问所有的点，求需要的最少时间，每一秒可以垂直移动，或水平移动，或沿对角线移动

**思考过程**

1. 沿对角线走是最省时的，因此考虑总是先沿着对角线移动，然后再水平或垂直移动，见法一

**具体代码**

法一
```JavaScript
var minTimeToVisitAllPoints = function(points) {
    let result = 0
    for (let i = 1; i < points.length; ++i) {
        // 前一个点
        let x1 = points[i-1][0]
        let y1 = points[i-1][1]
        // 后一个点
        let x2 = points[i][0]
        let y2 = points[i][1]
        // 计算水平和垂直距离
        let diffX = Math.abs(x2-x1)
        let diffY = Math.abs(y2-y1)
        // 沿着对角线移动
        result += Math.min(diffX, diffY)
        // 水平或垂直移动
        result += Math.abs(diffX-diffY)  
    }
    return result
}
```