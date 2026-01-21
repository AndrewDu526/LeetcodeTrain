# LC 19 删除链表的倒数第N个节点

## 1. Basic Information

- __level__: medium
- __time-cost__: n/a
- __completed-date__: 1-21-2026
- __completed-times__: 1
- __status__: 有思路，写不对

## 2. Solution

快慢指针构造“尺子”，快指针先走n步，接着双指针同时移动直到快指针触底，此时慢指针指向待删除节点的前节点（双指针起始于虚拟头节点），执行删除操作。

## 3. Code Implementation

    class Solution {
        public ListNode removeNthFromEnd(ListNode head, int n) {
            ListNode dummy = new ListNode(0, head);
            ListNode end = dummy;
            ListNode start = dummy;
    
            int i = 0;
            while(i<n){
                end = end.next;
                i++;
            }
    
            while(end.next!=null){
                end = end.next;
                start = start.next;
            }
    
            start.next = start.next.next;
            return dummy.next;
        }
    }

## 4. Notes

- 注意双指针需要在虚拟节点对齐。
