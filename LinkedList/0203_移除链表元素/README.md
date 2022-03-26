# 0203_移除链表元素

##   题目信息

[题目信息](https://leetcode-cn.com/problems/remove-linked-list-elements/)

给你一个链表的头节点 `head` 和一个整数 `val` ，请你删除链表中所有满足 `Node.val == val` 的节点，并返回 **新的头节点** 。

##   思路与题解

### 		    我的思路

* **指针遍历迭代**  创建指针，但要注意的是，考虑到题目要求删除所有值为 val 的节点，头节点也包含在内。不能和以往一样将指针p = head ，要另设一个 beforHead 节点，使这个新节点指向 head 并且使指针p = beforHead ，之前卡在这一步卡了好久。后面就是正常的判断删除

###     别人的题解

* **递归**  对于给定的链表，首先对除了头节点 head 以外的节点进行删除操作，然后判断 head 的节点值是否等于给定的 val。如果 head 的节点值等于 val，则 head 需要被删除，因此删除操作后的头节点为 head.next；如果 head 的节点值不等于 val，则 head 保留，因此删除操作后的头节点还是 head。上述过程是一个递归的过程。递归的终止条件是 head 为空，此时直接返回 head。当 head 不为空时，递归地进行删除操作，然后判断 head 的节点值是否等于 val 并决定是否要删除 head。


##   源码

* 指针遍历迭代

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode removeElements(ListNode head, int val) {
        //辅助指针
        ListNode beforHeader = new ListNode(-1);
        beforHeader.next = head;
        ListNode p = beforHeader;
        //遍历链表
        while(p.next != null){
            //找到待删除节点并删除
            if(p.next.val == val){
                p.next = p.next.next;
            }else{
                p = p.next;
            }
        }
        return beforHeader.next;
    }
}
```

* 递归

```java
class Solution {
    public ListNode removeElements(ListNode head, int val) {
        if (head == null) {
            return head;
        }
        head.next = removeElements(head.next, val);
        return head.val == val ? head.next : head;
    }
}
```

