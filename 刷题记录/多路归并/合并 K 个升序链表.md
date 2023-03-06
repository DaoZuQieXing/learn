#### <a href="https://leetcode.cn/problems/merge-k-sorted-lists/">合并 K 个升序链表</a>

-------------

```java
class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
        // 定义一个小根堆，里面存放每个链表的最小值
        PriorityQueue<ListNode> heap = new PriorityQueue<>(new Comparator<ListNode>() {
            @Override
            public int compare(ListNode o1, ListNode o2) {
                return o1.val - o2.val;
            }
        });
        for (ListNode node : lists) if (node != null) heap.add(node);
        
        ListNode dummy = new ListNode(-1);
        ListNode tail = dummy;
        while (!heap.isEmpty()) {
            ListNode node = heap.poll();
            
            tail = tail.next = node;
            if (node.next != null) heap.add(node.next);
        }
        return dummy.next;
    }
}
```

