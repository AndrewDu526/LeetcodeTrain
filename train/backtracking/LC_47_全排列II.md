# LC 47 全排列II

## 1. Basic Information

- __level__: medium
- __time-cost__: 未计时
- __completed-date__: 12-27-2025
- __completed-times__: 1
- __status__: 卡在去重，GPT纠错协助完成，困难

## 2. Solution

先排序再用Set或者boolean 数组去重，重点在于startindex固定为0，需要区分纵向递归和横向遍历的重复元素，仅删除后者。

## 3. Code Implementation

    class Solution {
        List<List<Integer>> result = new ArrayList<>();
        List<Integer> path = new ArrayList<>();
        Set<Integer> record = new HashSet<>();
    
        public List<List<Integer>> permuteUnique(int[] nums) {
            Arrays.sort(nums);
            backtracking(nums);
            return result;
        }
    
        private void backtracking(int[] nums){
                if(path.size()==nums.length){
                    result.add(new ArrayList<>(path));
                    return;
                }
        
                for(int i=0;i<nums.length;i++){
    
                    if(i>0 && nums[i]==nums[i-1] && !record.contains(i-1)){continue;}
                    if (record.contains(i)) continue;
                    
                    path.add(nums[i]);
                    record.add(i);
                    backtracking(nums);
                    record.remove(i);
                    path.remove(path.size()-1);
                }
            }
    }

## 4. Notes

- 排列去重问题，目标是删除同层横向重复、保留纵向递归合法路径。由于排列中每一层 for 都从 0 开始遍历同一个数组，相同元素既可能出现在同一层横向，也可能出现在不同层纵向，因此不能仅通过值判断去重。解决方法是：当当前元素与前一个相同且前一个元素不在 path 中时，说明仍处于同一层横向遍历，应剪枝；若前一个相同元素已在 path 中，则属于纵向递归，应保留。
- 为避免纵向递归中重复使用同一元素，需要额外判断当前下标（而非元素本身）是否已被使用。
- 与组合/子集类回溯不同，后者通过 startIndex 递增天然区分层级，相同元素只会在同层出现，因此无需区分横向与纵向。
- 实现上可使用 HashSet 或 boolean[] used 记录下标使用情况，后者更简洁高效。
