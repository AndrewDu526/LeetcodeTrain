# LC 63 不同路径II

## 1. Basic Information

- __level__: mid
- __time-cost__: n/a
- __completed-date__: 2-3-2026
- __completed-times__: 1
- __status__: fail

## 2. Solution

不同路径解题一致，核心是保持有障碍的位置为0，注意初始化时的排查

## 3. Code Implementation

    class Solution {
        public int uniquePathsWithObstacles(int[][] obstacleGrid) {
            int m = obstacleGrid.length;
            int n = obstacleGrid[0].length;
            int[][] dp = new int[m][n];
    
            //如果在起点或终点出现了障碍，直接返回0
            if (obstacleGrid[m - 1][n - 1] == 1 || obstacleGrid[0][0] == 1) {
                return 0;
            }
    
            for (int i = 0; i < m && obstacleGrid[i][0] == 0; i++) {
                dp[i][0] = 1;
            }
            for (int j = 0; j < n && obstacleGrid[0][j] == 0; j++) {
                dp[0][j] = 1;
            }
    
            for (int i = 1; i < m; i++) {
                for (int j = 1; j < n; j++) {
                    dp[i][j] = (obstacleGrid[i][j] == 0) ? dp[i - 1][j] + dp[i][j - 1] : 0;
                }
            }
            return dp[m - 1][n - 1];
        }
    }


## 4. Notes

- 注意new int[m][n]时将把元素初始化为0
