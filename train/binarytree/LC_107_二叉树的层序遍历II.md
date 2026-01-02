# LC 

## 1. Basic Information

- __level__: medium
- __time-cost__: 未计时
- __completed-date__: 1-2-2026
- __completed-times__: 1
- __status__: 生疏的独立完成

## 2. Solution

我的方法：层序遍历后翻转数组

## 3. Code Implementation

    class Solution {
        List<List<Integer>> result = new ArrayList<>();
    
        public List<List<Integer>> levelOrderBottom(TreeNode root) {
            travel02(root, 0);
            List<List<Integer>> temp = new ArrayList<>();
            for(int i=result.size()-1;i>=0;i--){
                temp.add(result.get(i));
            }
    
            return temp;
        }
    
        private void travel02(TreeNode node, int deep){
            if(node == null){return;}
    
            deep++;
    
            if(result.size()<deep){
                result.add(new ArrayList<>());
            }
    
            result.get(deep-1).add(node.val);
    
            travel02(node.left, deep);
            travel02(node.right, deep);
        }
    }

## 4. Notes

- 偷懒了
