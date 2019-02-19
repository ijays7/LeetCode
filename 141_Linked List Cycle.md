## Linked List Cycle

Given a linked list, determine if it has a cycle in it.

![](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist.png)

## Solution

这道题是判断链表中是否有环。

这道题的思路是使用快慢指针，其中慢指针每次只移动1步，快指针每次移动2步，如果在移动的过程中，两个指针相遇了，那么则可以断定链表中存在环。

```java
  public boolean hasCycle(ListNode head) {

        if (head == null) {
            return false;
        }

        ListNode nodeNext1 = head;
        ListNode nodeNext2 = head;

        while (nodeNext1.next != null && nodeNext2.next != null
                && nodeNext2.next.next != null) {
            nodeNext1 = nodeNext1.next;
            nodeNext2 = nodeNext2.next.next;

            if (nodeNext1 == nodeNext2) {
                return true;
            }
        }

        return false;
    }
```

