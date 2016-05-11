# Merge Two Sorted Lists
## 描述
Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.
## 分析
设置两个指针，分别指向两个链表，比较元素大小，交替地把较小元素连接到返回链表的尾部。直到到某个链表的尾部，然后把剩下的那个链表链接到返回链表的尾部，结束。
## 代码实现

```java
public class MergeTwoSortedLists {
    // Definition for singly-linked list.
    public static class ListNode {
        int val;
        ListNode next;
        ListNode(int x) {
            val = x;
        }
    }

    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        if (l1 == null || l2 == null) {
            return l1 != null ? l1 : l2;
        }
        ListNode head = new ListNode(-1);
        ListNode cur = head;
        while (l1 != null && l2 != null) {
            if (l1.val < l2.val) {
                cur.next = l1;
                cur = cur.next;
                l1 = l1.next;
            } else {
                cur.next = l2;
                cur = cur.next;
                l2 = l2.next;
            }
        }
        cur.next = l1 != null ? l1 : l2;

        return head.next;
    }
```
