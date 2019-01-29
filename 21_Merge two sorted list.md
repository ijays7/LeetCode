## Merge two sorted list

Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

**Example:**

```
Input: 1->2->4, 1->3->4
Output: 1->1->2->3->4->4
```

## Solution

```java
public  ListNode mergeTwoLists(ListNode l1, ListNode l2) {

        if (l1 == null && l2 == null) {
            return null;
        }
        if (l1 == null) {
            return l2;
        }
        if (l2 == null) {
            return l1;
        }

        // 虚拟头节点
        ListNode dummyHead = new ListNode(0);
        // 指向链表的尾部
        ListNode cur = dummyHead;
        while (l1 != null && l2 != null) {
            if (l1.value > l2.value) {
                cur.next = l2;
                l2 = l2.next;

            } else {
                cur.next = l1;
                l1 = l1.next;
            }
            cur = cur.next;
        }

        // 此时如果l1或者l2中还有元素，直接加载尾部
        if (l1 != null) {
            cur.next = l1;
        }
        if (l2 != null) {
            cur.next = l2;
        }
        return dummyHead.next;
    }
```

