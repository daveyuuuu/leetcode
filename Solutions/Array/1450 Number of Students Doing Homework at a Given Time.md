**题目理解**

- 给定两个数组，startTime和endTime，和一个查询时间queryTime，数组中的每个元素代表的是第i个学生开始做作业和结束做作业的时间，问在查询的时间那一刻有多少个学生在做作业？

**思考过程**

1. 即问queryTime属于多少个startTime->endTime，闭区间，直接进行遍历比较，见法一

**具体代码**

法一
```javascript
var busyStudent = function(startTime, endTime, queryTime) {
  let result = 0
  for (let i = 0; i < startTime.length; ++i) {
    if (startTime[i] <= queryTime && endTime[i] >= queryTime) {
      result++
    }
  }
  return result
}
```
