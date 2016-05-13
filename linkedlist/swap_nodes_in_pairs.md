# Swap Nodes in Pairs

##分析 
同反转链表等题目一样，仔细分析，设置好指针的交换顺序。
## 代码实现
```java
    public ListNode swapPairs(ListNode head) {
        ListNode dummy = new ListNode(-1);
        dummy.next = head;
        ListNode prev = dummy;
        ListNode first = dummy.next;
        while (first!= null && first.next != null) {
            prev.next = first.next;
            first.next = first.next.next;
            prev.next.next = first;

            prev=first;
            first = first.next;
        }
        return dummy.next;
    }
```