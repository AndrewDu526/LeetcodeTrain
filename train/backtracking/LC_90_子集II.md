# LC 90 子集II

## 1. Basic Information

- __level__: medium
- __time-cost__: 未计时
- __completed-date__: 12-27-2025
- __completed-times__: 1
- __status__: 独立完成

## 2. Solution

思路和组合总数II的同层去重一样

## 3. Code Implementation

    class Solution {
    
        List<List<Integer>> result = new ArrayList<>();
        List<Integer> node = new ArrayList<>();
    
        public List<List<Integer>> subsetsWithDup(int[] nums) {
            Arrays.sort(nums);
    
            backtracking(nums, 0);
            result.add(new ArrayList<>());
            return result;
        }
    
        private void backtracking(int[] nums, int index){
            for(int i=index;i<nums.length;i++){
                if(i>index && nums[i]==nums[i-1]){
                    continue;
                }
    
                node.add(nums[i]);
                result.add(new ArrayList<>(node));
                backtracking(nums, i+1);
                node.remove(node.size()-1);
            }
        }
    }

## 4. Notes

- 注意二维ArrayList增加元素需要new一个ArrayList，不能直接传递path
