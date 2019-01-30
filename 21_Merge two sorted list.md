## Merge two sorted list

Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

**Example:**

```
Input: 1->2->4, 1->3->4
Output: 1->1->2->3->4->4
```

## Solution

这道题是合并两个已经排好序的 list，并将其返回。一开始我想直接在 l1 的基础上一个一个将 l2 的元素插进去，但显然这样是不行。在 Youtube 上看到下面的方法比较高明，6ms，在 Java 提交的代码里算相当好的成绩了，于是记录下这个方法。

我们创建一个 dummyHead (暂且翻译为虚拟节点吧)，同时 new 一个 cur 指针指向 dummyHead。接下来我们循环 L1 和 L2 链表，比较其 value 的大小，然后将 cur 指针指向大小较小 value 所在的链表，即 cur 指针永远指向的都是链表的尾部。比如：L1 为 -1->0->1，L2 为 1->2->3，在进行第一次比较时，比较 -1 和 1 的大小，因为 1 > -1，所以我们将 cur 指向 L1，并且移动 L1 的指针。最后结束循环后，可能由于两个链表的长度不同，导致结束循环后，L1 和 L2 仍然还是元素剩余，这个时候我们只需将剩余的元素拼接上即可。

这样做的时间复杂度为 O( m+n )。

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

