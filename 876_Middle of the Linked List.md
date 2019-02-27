## Middle of the Linked List

Given a non-empty, singly linked list with head node `head`, return a middle node of linked list.

If there are two middle nodes, return the second middle node.

 

**Example 1:**

```
Input: [1,2,3,4,5]
Output: Node 3 from this list (Serialization: [3,4,5])
The returned node has value 3.  (The judge's serialization of this node is [3,4,5]).
Note that we returned a ListNode object ans, such that:
ans.val = 3, ans.next.val = 4, ans.next.next.val = 5, and ans.next.next.next = NULL.
```

## Solution

这道题是给定一个非空的单链表，返回链表中间的节点。

这道题思路很简单，首先遍历一遍链表，得到链表的长度，然后找到中间的地方，最后遍历链表到中间的地方。

时间复杂度为 O(n)，空间复杂度为 O(1)。

```java
 public ListNode middleNode(ListNode head) {
         int count = 0;
        int countFlag = 0;

        ListNode iteration = head;

        while (iteration != null) {
            count++;
            iteration = iteration.next;
        }
        if (count % 2 == 0) {
            count = count / 2;
        } else {
            count = count / 2;
        }

        while (countFlag < count) {
            countFlag++;
            head = head.next;
        }
        return head;
    }
```

