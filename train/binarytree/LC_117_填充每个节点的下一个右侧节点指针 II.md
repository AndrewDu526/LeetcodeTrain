# LC 117 填充每个节点的下一个右侧节点指针 II

## 1. Basic Information

- __level__: medium
- __time-cost__: 未计时
- __completed-date__: 1-1-2026
- __completed-times__: 1
- __status__: 独立完成

## 2. Solution

由于层序遍历bfs，和116解法一摸一样

## 3. Code Implementation

    class Solution {
        public Node connect(Node root) {
            Queue<Node> que = new ArrayDeque<>();
    
            if(root == null){return null;}
    
            que.offer(root);
    
            while(!que.isEmpty()){
                int size = que.size();   
                for(int i=size;i>0;i--){
                    Node node = que.poll();
    
                    if (i == 1) node.next = null;
                    else node.next = que.peek();
    
                    if(node.left != null){que.offer(node.left);}
                    if(node.right != null){que.offer(node.right);}
                }
            }
    
            return root;
        }
    }

## 4. Notes

- 研究其他更好解法
