# 0206_反转链表

##   题目信息

[题目信息](https://leetcode-cn.com/problems/reverse-linked-list/)

给你单链表的头节点 `head` ，请你反转链表，并返回反转后的链表。

##   思路与题解

### 		    我的思路

* **迭代插入**  创建指针，与反向链表头节点，每一次遍历时，都把指针指向（`next`改为）反向链表头节点的下一节点，同时让反向链表的头节点指向修改过的指针，从而形成`reversHead -> cur -> 尾部 -> null`的结构，即插入。遍历完成后返回新链表。

###     别人的题解

* **递归**  [明白那一步`head.next.next = head`就好理解了](https://leetcode-cn.com/problems/reverse-linked-list/solution/dong-hua-yan-shi-206-fan-zhuan-lian-biao-by-user74/)

* 递归的两个条件：

  1. 终止条件是当前节点或者下一个节点==null
  2. 在函数内部，改变节点的指向，也就是 head 的下一个节点指向 head 递归函数那句

  递归函数中每次返回的 cur 其实只是最后一个节点，在递归函数内部，改变的是当前节点的指向。


##   源码

* 迭代插入

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
    public ListNode reverseList(ListNode head) {
        //如果当前链表为空，或者只有一个节点，无需反转，直接返回
        if(head == null || head.next == null) {
            return head;
        }

        ListNode cur = head;
        ListNode next = null;// 指向当前节点[cur]的下一个节点
        ListNode reverseHead = new ListNode(-1);
        //遍历原来的链表，每遍历一个节点，就将其取出，并放在新的链表reverseHead 的最前端
        while(cur != null){
            next = cur.next;//先暂时保存当前节点的下一个节点，因为后面需要使用
            cur.next = reverseHead.next;//将cur的下一个节点指向新的链表的最前端
            reverseHead.next = cur; //将cur 连接到新的链表上
            cur = next;//让cur后移
        }

        return reverseHead.next;
    }
}
```

* 递归

```java
class Solution {
	public ListNode reverseList(ListNode head) {
		//递归终止条件是当前为空，或者下一个节点为空
		if(head==null || head.next==null) {
			return head;
		}
		//这里的cur就是最后一个节点
		ListNode cur = reverseList(head.next);
		//这里请配合动画演示理解
		//如果链表是 1->2->3->4->5，那么此时的cur就是5
		//而head是4，head的下一个是5，下下一个是空
		//所以head.next.next 就是5->4
		head.next.next = head;
		//防止链表循环，需要将head.next设置为空
		head.next = null;
		//每层递归函数都返回cur，也就是最后一个节点
		return cur;
	}
}
```

