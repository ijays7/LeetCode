## Intersection of Two Linked Lists

Write a program to find the node at which the intersection of two singly linked lists begins.

**Example 1:**

![img](https://assets.leetcode.com/uploads/2018/12/13/160_example_1.png)



```
Input: intersectVal = 8, listA = [4,1,8,4,5], listB = [5,0,1,8,4,5], skipA = 2, skipB = 3
Output: Reference of the node with value = 8
Input Explanation: The intersected node's value is 8 (note that this must not be 0 if the two lists intersect). From the head of A, it reads as [4,1,8,4,5]. From the head of B, it reads as [5,0,1,8,4,5]. There are 2 nodes before the intersected node in A; There are 3 nodes before the intersected node in B.
```

## Solution

这道题是给定两个链表，需要返回两个链表相重叠的部分，如果没有，则返回 null。

这道题首先想到的就是暴力破解。其实最多了才发现其实链表的题相比于其他类型的题目套路比较固定，变化相对较少。说回解法，使用两个指针 pA，pB 分别 指向 headA 和 headB，然后循环移动指针，判断是否找到相等。

这个做法的话时间复杂度是 O(m+n)，空间复杂度为 O(1)，满足题意。

```java
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
         if (headA == null || headB == null) {
            return null;
        }

        ListNode pA = headA;
        ListNode pB = headB;

        while (pA != pB) {
            if (pA == null) {
                pA = headA;
            } else {
                pA = pA.next;
            }

            if (pB == null) {
                pB = headB;
            } else {
                pB = pB.next;
            }
        }

        return pA;
    }
```

提交之后惯例看了最快的代码，令人吃惊的是，上面的代码只改了两个引用，即在循环中判断当 pA 为 null 时，将 pA 指向 headB，同理，将 pB 指向 headA，这样做居然只用了1ms。这个技巧两人叹为观止。

```java
  public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        if (headA == null || headB == null) {
            return null;
        }

        ListNode pA = headA;
        ListNode pB = headB;

        while (pA != pB) {
            if (pA == null) {
                pA = headA;
            } else {
                pA = pA.next;
            }

            if (pB == null) {
                pB = headB;
            } else {
                pB = pB.next;
            }
        }

        return pA;
    }
```



