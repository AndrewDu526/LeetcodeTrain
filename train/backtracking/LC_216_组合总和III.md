# LC 216 组合总和III

## 1. Basic Information

- __level__: medium
- __time-cost__: 未计时
- __completed-date__: 12-28-2025
- __completed-times__: 1
- __status__: 秒了

## 2. Solution

横向遍历跟踪的集合固定为2-9，简单。

## 3. Code Implementation

    class Solution {
    
        List<List<Integer>> result = new ArrayList<>();
        List<Integer> path = new LinkedList<>();
    
        public List<List<Integer>> combinationSum3(int k, int n) {
            
            int sum = 0;
            backtracking(k, n, sum, 1);
            return result;
        }
    
        private void backtracking(int k, int n, int sum, int index){
            if(path.size()==k && sum==n){
                result.add(new ArrayList<>(path));
                return;
            }
    
            for(int i=index;i<=9;i++){
                path.add(i);
                sum+=i;
                backtracking(k, n, sum, i+1);
                sum-=i;
                path.remove(path.size()-1);
            }
        }
    }

## 4. Notes

- 希望每道回溯都这样
