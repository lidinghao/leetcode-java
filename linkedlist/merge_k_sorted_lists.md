# Merge k Sorted Lists
## 问题描述
Merge k sorted linked lists and return it as one sorted list. Analyze and describe its complexity.
## 分析
这个归并排序的第二个步骤是一样的，对k个链表进行两两归并，然后在对产生的k/2个链表再进行两两归并，直到最终归并到一个链表。时间复杂度为(nlgk),n为链表的最大长度
或者维护一个k大小的小根堆，不断地取走堆顶元素，并将该元素的next节点插入堆中，直至堆为空，即所有链表都遍历完。时间复杂度为(nlgk),n为链表的最大长度。
## 代码实现

**递归两两归并版**
```java
    public ListNode mergeKLists(ListNode[] lists) {
        if (lists.length == 0) return null;
        if (lists.length == 1) return lists[0] ;
        ListNode[] newLists = new ListNode[(lists.length + 1) / 2];
        for (int i = 0; i < lists.length / 2; i++) {
            ListNode node = mergeTwoLists(lists[2*i], lists[2*i + 1]);
            newLists[i] = node;
        }
        if (lists.length %2 != 0) newLists[(lists.length + 1) / 2 - 1] = lists[lists.length - 1];
        return mergeKLists(newLists);
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

**最小堆版**
```
public ListNode mergeKListsV2(ListNode[] lists) {
        if (lists.length == 0) {
            return null;
        }
        PriorityQueue<ListNode> minHeap = new PriorityQueue<>(lists.length, 
        new Comparator<ListNode>() {
            @Override
            public int compare(ListNode o1, ListNode o2) {
                if (o1.val < o2.val) {
                    return  -1;
                } else if (o1.val == o2.val) {
                    return 0;
                } else {
                    return 1;
                }
            }
        });

        for (ListNode list : lists) {
            if (list != null) {
                minHeap.add(list);
            }
        }
        ListNode head = new ListNode(-1);
        ListNode tail = head;
        while (!minHeap.isEmpty()) {
            tail.next = minHeap.poll();
            tail = tail.next;
            if (tail.next != null)
            minHeap.add(tail.next);
        }
        return head.next;
    }
```
