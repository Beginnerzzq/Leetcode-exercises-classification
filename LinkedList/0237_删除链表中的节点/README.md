# 0237_删除链表中的节点

##   题目信息

[题目信息](https://leetcode-cn.com/problems/delete-node-in-a-linked-list/)

给你一个单链表的头节点 `head` ，请你判断该链表是否为回文链表。如果是，返回 `true` ；否则，返回 `false` 。

##   思路与题解

### 		    我的思路

* 引用别人的一句话，一语惊醒梦中人

  这道题是有点属于急转弯了，存粹为了做题而出题了。 node这个节点就是需要删除的节点；之前我们可以用head->next->val去判断下一个是否是删除的节点，然后head->next=head->next->next，这题可以用把 node下一节点复制到node，把下一节点跳过！变通，这道题出的挺有意思的！


##   源码

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public void deleteNode(ListNode node) {
        ListNode temp = node;
        node.val = temp .next.val;
        node.next = temp.next.next;
    }
}
```
