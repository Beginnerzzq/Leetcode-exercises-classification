# 1290_二进制链表转整数

##   题目信息

[题目信息](https://leetcode-cn.com/problems/convert-binary-number-in-a-linked-list-to-integer/)

给你一个单链表的引用结点 head。链表中每个结点的值不是 0 就是 1。已知此链表是一个整数数字的二进制表示形式。

请你返回该链表所表示数字的 十进制值 。

##   思路与题解

### 		    我的思路

* 调用`Integer.valueOf()`方法，拼接字符串后直接转为十进制数。提交代码后发现，用时达到了惊人的10ms，内存消耗更是大的惊人。简而言之，我的代码很垃圾。

###     别人的题解

* **利用栈**

  我最初想法也是想用一个数组或者字符串，把这些节点值进行储存，然后只需要考虑怎么把二进制转为十进制就行了。但是我没有想到一个

* **利用数学公式**

  ```txt
  5÷2=2余1 
  2÷2=1余0 
  1÷2=0余1  
   ===> 得出二进制 101 .
  反推回去 商 x 除数 + 余数 
  => 0 x 2 + 1 = 1 
  -> 1 x 2 + 0 = 2
  -> 2 x 2 +1 = 5
  ```

##   源码

* 调用`Integer.valueOf()`方法

```java
class Solution {
    public int getDecimalValue(ListNode head) {
        ListNode cur = head;
        String str = "";
        while(cur != null){
            str += cur.val; 
            cur = cur.next;
        }
        return Integer.valueOf(str,2);
    }
}
```

* 利用栈

```java
class Solution {
    public int getDecimalValue(ListNode head) {
		if (head == null)
			return 0;
		Stack<Integer> stack = new Stack<>();
		while (head != null) {
			stack.push(head.val);
			head = head.next;
		}
		int mark = 1;
		int ans = 0;
		while (!stack.isEmpty()) {
			ans += stack.pop() * mark;
			mark <<= 1;
		}
		return ans;
    }
}
```

* 利用数学公式

```java
class Solution {
    public int getDecimalValue(ListNode head) {
        ListNode curNode = head;
        int ans = 0;
        while (curNode != null) {
            ans = ans * 2 + curNode.val;
            curNode = curNode.next;
        }
        return ans;
    }
}
```

