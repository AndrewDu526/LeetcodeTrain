# LC 40 组合总和II

## 1. Basic Information

- __level__: medium
- __time-cost__: null 
- __completed-date__: 12-27-2025
- __completed-times__: 1
- __status__: 在GPT纠错下完成

## 2. Solution

for循环内用if的i>index实现同层去重

## 3. Code Implementation

    class Solution {
        List<List<Integer>> result = new ArrayList<>();
        List<Integer> path = new ArrayList<>();
    
        public List<List<Integer>> combinationSum2(int[] candidates, int target) {
            Arrays.sort(candidates);
    
            backtracking(candidates, target, 0, 0);
            return result;
        }
    
        private void backtracking(int[] candidates, int target, int sum, int index){
            if(sum == target){
                result.add(new ArrayList<>(path));
                return;
            }else if(sum >= target){
                return;
            }
    
            for(int i=index;i<candidates.length;i++){
    
                if(i>index && candidates[i]==candidates[i-1]){
                    continue;
                }
    
                sum+=candidates[i];
                path.add(candidates[i]);
                backtracking(candidates, target, sum, i+1);
                path.remove(path.size()-1);
                sum-=candidates[i];
            }
        }
    }

## 4. Notes

- for循环保证处于同一层操作，内部对同层相同元素去重，先排序。
