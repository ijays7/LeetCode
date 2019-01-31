## Remove Duplicates From Sortes List

Given a sorted linked list, delete all duplicates such that each element appear only *once*.

**Example 1:**

```
Input: 1->1->2
Output: 1->2
```

## Solution

这道题主要是考察对于链表指针操控的熟练程度，本身也并没有太多的思维复杂程度。思路也比较直接，即遍历整个链表，当发现某个节点的 value 等于我们的 val 时候，移动指针指向下一个元素。最后我们再判断一下如果头指针的 value 也等于 val 的时候，直接移动头指针指向下一个节点。

Java version:

```java
public ListNode removeElements(ListNode head, int val) {
         if (head == null) {
            return null;
        }
        
        ListNode current = head;

        while (current.next != null) {
            if (current.next.val == val) {
                current.next = current.next.next;
            } else {
                current = current.next;
            }
        }

        if (head.val == val) {
            return head.next;
        }

        return head;
    }

```

Kotlin version:

```kotlin
 fun removeElements(head: ListNode?, `val`: Int): ListNode? {
        if (head == null) {
        return null
    }

    val replica = head
    var dummyHead = replica

    while (dummyHead?.next != null) {
        if (dummyHead.next?.`val`==`val`){
            dummyHead.next = dummyHead.next?.next

        } else {
            dummyHead = dummyHead.next
        }
    }

    if (replica?.`val` == `val`) {
        return replica.next
    }

    return replica
    }
```

