**题目理解**

- 给定一个二维矩阵，值为1代表陆地，值为0代表书面，让你求整个陆地的周长，保证只有一片陆地（若干个1连接），细节见题目图片

**思考过程**

1. 每片陆地周长为4，没与其他陆地连接自己的周长就少1，遍历所有的陆地，若有相连就减1，见法一

2. 用DFS遍历每一个为1的陆地，将当前值置为其他数字，若碰到边界或水面，周长加1，碰到陆地则不动，继续遍历，见法二
**具体代码**

法一
```javascript
var islandPerimeter = function(grid) {
  let result = 0
  for (let i = 0; i < grid.length; ++i) {
    for (let j = 0; j < grid[0].length; ++j) {
      if (grid[i][j] === 1) {
        result += 4
        let connect = (i-1 >= 0 && grid[i-1][j] === 1)
          + (i+1 < grid.length && grid[i+1][j] === 1)
          + (j-1 >= 0 && grid[i][j-1] === 1)
          + (j+1 < grid[i].length && grid[i][j+1] === 1)
        result -= connect
      }
    }
  }
  return result
}
```

法二
```javascript
var islandPerimeter = function(grid) {
  function dfs(grid, i, j) {
    if (i < 0 || i >= grid.length || j < 0 || j >= grid[i].length) {
      return 1
    }
    if (grid[i][j] === 0) {
      return 1
    }
    if (grid[i][j] === -1) {
      return 0
    }
    let count = 0
    grid[i][j] = -1
    count += dfs(grid, i + 1, j)
    count += dfs(grid, i - 1, j)
    count += dfs(grid, i, j + 1)
    count += dfs(grid, i, j - 1)
    return count
  }
  for (let i = 0 ; i < grid.length; ++i) {
    for (let j = 0; j < grid[i].length; ++j) {
      if (grid[i][j] === 1) {
        return dfs(grid, i, j)
      }
    }
  }
}
```