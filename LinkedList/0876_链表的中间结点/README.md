# 0876_链表的中间结点

##   题目信息

[题目信息](https://leetcode-cn.com/problems/palindrome-linked-list/)

给你一个单链表的头节点 `head` ，请你判断该链表是否为回文链表。如果是，返回 `true` ；否则，返回 `false` 。

##   思路与题解

### 		    我的思路

* **快慢指针法**  （和单指针法比起来，这道题我的双指针有点没事找事）

  找到中点后，链表数为奇则返回slow，偶则返回slow.next

###     别人的题解

* **单指针法**

  我们可以对链表进行两次遍历。第一次遍历时，我们统计链表中的元素个数 N；第二次遍历时，我们遍历到第 N/2 个元素（链表的首节点为第 0 个元素）时，将该元素返回即可。

* **快慢指针法（优化）**

  很妙。改变了while遍历的判定条件，有点使快指针强行多往后指一位的意图，达到题意的要求。

##   源码

* 快慢指针法

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
    public ListNode middleNode(ListNode head) {
        int count = 0;//记录链表节点个数
        ListNode cur = head;
        ListNode slow = head;
        ListNode fast = head;
        while(cur != null){
            count += 1;
            cur = cur.next;
        }

        while(fast.next != null && fast.next.next != null){
            slow = slow.next;
            fast = fast.next.next;
        }

        if(count % 2 == 0){
            return slow.next;
        }else{
            return slow;
        }
    }
}
```

* 单指针法

```java
class Solution {
    public ListNode middleNode(ListNode head) {
        int n = 0;
        ListNode cur = head;
        while (cur != null) {
            ++n;
            cur = cur.next;
        }
        int k = 0;
        cur = head;
        while (k < n / 2) {
            ++k;
            cur = cur.next;
        }
        return cur;
    }
}
```

* 快慢指针法（优化）

```java
class Solution {
    public ListNode middleNode(ListNode head) {
        ListNode slow = head, fast = head;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        return slow;
    }
}
```

