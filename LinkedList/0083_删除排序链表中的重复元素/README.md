# 0083_删除排序排序链表中的重复元素

## 题目信息

[题目信息](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list/)

给定一个已排序的链表的头 `head` ， *删除所有重复的元素，使每个元素只出现一次* 。返回 *已排序的链表* 。

## 思路与题解

### 		我的思路

* 判断当前节点是否与前节点值是否相同，相同则跳过，不同则递归
* 下一节点为空时，递归结束

### 		反思

* 在做题过程中发现用例 [1,1,1] 通过不了，经查询，发现大佬的递归多一行`return deleteDuplicates(head);`（源码21行）加上这行，才得以运行成功。这行代码原理是java的递归调用机制。
* 官方给出的题解中用到了辅助节点遍历，遍历一遍之后删除相同节点。

## 源码

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
    public ListNode deleteDuplicates(ListNode head) {
        if(head == null)
            return null;
        if(head.next == null)
            return head;

        if(head.val == head.next.val){
            //相同则跳过
            head.next = deleteDuplicates(head.next.next);
            return deleteDuplicates(head);
        }else{
            //不同则递归
            head.next = deleteDuplicates(head.next);
        }

        return head;
    }
}
```

