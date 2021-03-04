---
layout: post
title:  "24. 两两交换链表中的节点"
date:   2020-2-28 22:30:00
categories: LeetCode
---
题目描述

    给定一个链表，两两交换其中相邻的节点，并返回交换后的链表。
    你不能只是单纯的改变节点内部的值，而是需要实际的进行节点交换。
    
    示例:
        输入：head = [1,2,3,4]
        输出：[2,1,4,3]

#### 解题思路
虽然也是要用迭代的思想，但是记录结果集的根节点和两两迭代都写得太复杂了，容易导致死循环。
```java
public class SwapNodesInPairs {

    public ListNode swapPairs(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        ListNode ans = head.next;
        ListNode last = head;
        ListNode next = ans.next;
        ans.next = last;
        last.next = null;

        while (next != null && next.next != null) {
            ListNode first = next;
            ListNode second = next.next;
            ListNode temp = second.next;

            last.next = second;
            second.next = first;

            last = first;
            last.next = null;
            next = temp;
        }
        if (next != null) {
            last.next = next;
        }
        return ans;
    }

}
```

#### 官方解答
方法一：递归
两两交换，所以发生变化的是相邻的两个节点，故每两个节点形成一次递归。
时间复杂度：O(n)，n是链表的节点数量。
空间复杂度：O(n)，空间复杂度主要取决于递归调用的栈空间。
```java
public ListNode swapPairs(ListNode head) {
    if (head == null || head.next == null) {
        return head;
    }
    ListNode newHead = head.next;
    head.next = swapPairs(newHead.next);
    newHead.next = head;
    return newHead;
}
```

方法二：迭代
亮点在于创建虚拟根节点，后续两两迭代交换即可，两两迭代的三要素：当前节点的copy，后一个节点的copy，临时节点。
时间复杂度：O(n)
空间复杂度：O(1)
```java
public ListNode swapPairs(ListNode head) {
        ListNode dummyHead = new ListNode(0);
        dummyHead.next = head;
        ListNode temp = dummyHead;
        while (temp.next != null && temp.next.next != null) {
            ListNode node1 = temp.next;
            ListNode node2 = temp.next.next;
            temp.next = node2;
            node1.next = node2.next;
            node2.next = node1;
            temp = node1;
        }
        return dummyHead.next;
    }
```

#### 小结
在做链表的元素变化题时，可创建临时根节点来记录结果集的根元素。


leetcode原题链接：[24. 两两交换链表中的节点](https://leetcode.com/problems/swap-nodes-in-pairs/)