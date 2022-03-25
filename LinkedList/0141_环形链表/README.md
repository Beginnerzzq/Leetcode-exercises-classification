# 0141_环形链表题目信息

## 题目信息

[题目信息](https://leetcode-cn.com/problems/linked-list-cycle/)

给你一个链表的头节点 head ，判断链表中是否有环。

如果链表中有某个节点，可以通过连续跟踪 next 指针再次到达，则链表中存在环。 为了表示给定链表中的环，评测系统内部使用整数 pos 来表示链表尾连接到链表中的位置（索引从 0 开始）。注意：pos 不作为参数进行传递 。仅仅是为了标识链表的实际情况。

如果链表中存在环 ，则返回 true 。 否则，返回 false 。

## 思路与题解

### 		我的思路

* 我是fw。题都没看懂，单纯的以为 pos 大于0就可以判定为有环。下面的大佬的解答

### 		别人的题解

* 可以使用**快慢指针法**， 分别定义 fast 和 slow 指针，从头结点出发，fast 指针每次移动两个节点，slow 指针每次移动一个节点，如果 fast 和 slow 指针在途中相遇 ，说明这个链表有环。

* **哈希表**：最容易想到的方法是遍历所有节点，每次遍历到一个节点时，判断该节点此前是否被访问过。

  具体地，我们可以使用哈希表来存储所有已经访问过的节点。每次我们到达一个节点，如果该节点已经存在于哈希表中，则说明该链表是环形链表，否则就将该节点加入哈希表中。重复这一过程，直到我们遍历完整个链表即可。


## 源码

* 快慢指针法

```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public boolean hasCycle(ListNode head) {
		ListNode fast = head;
		ListNode slow = head;
		// 空链表、单节点链表一定不会有环
		while (fast != null && fast.next != null) {
			fast = fast.next.next; // 快指针，一次移动两步
			slow = slow.next;      // 慢指针，一次移动一步
			if (fast == slow) {   // 快慢指针相遇，表明有环
				return true;
			}
		}
		return false; // 正常走到链表末尾，表明没有环
    }
}
```

* 哈希表（没看懂）

```java
public class Solution {
    public boolean hasCycle(ListNode head) {
        Set<ListNode> seen = new HashSet<ListNode>();
        while (head != null) {
            if (!seen.add(head)) {
                return true;
            }
            head = head.next;
        }
        return false;
    }
}
```

