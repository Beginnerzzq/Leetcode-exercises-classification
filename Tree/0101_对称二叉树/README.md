# 0101_对称二叉树

##   题目信息

[题目信息](https://leetcode-cn.com/problems/symmetric-tree/)

给你一个二叉树的根节点 `root` ， 检查它是否轴对称。

##   思路与题解

### 		    我的思路

* **递归**

  递归的方法很好理解，就不介绍了

###     别人的题解

* **迭代**

  递归中我们用递归的方法实现了对称性的判断，那么如何用迭代的方法实现呢？首先我们引入一个队列，这是把递归程序改写成迭代程序的常用方法。初始化时我们把根节点入队两次。每次提取两个结点并比较它们的值（队列中每两个连续的结点应该是相等的，而且它们的子树互为镜像），然后将两个结点的左右子结点按相反的顺序插入队列中。当队列为空时，或者我们检测到树不对称（即从队列中取出两个不相等的连续结点）时，该算法结束。



##   源码

* 递归

```java
class Solution {
    public boolean isSymmetric(TreeNode root) {
        return compare(root.left, root.right);
    }

    private boolean compare(TreeNode left,TreeNode right){
        boolean res = false;
        if(left == null && right == null)
            return true;

        if(left == null && right != null){
            return false;
        }
        if(left != null && right == null){
            return false;
        }

        if(left.val == right.val){
            res = compare(left.left, right.right);
            if(res){
                res = compare(left.right, right.left);
            }
        }

        return res;
    }
}
```

* 迭代

```java
class Solution {
    public boolean isSymmetric(TreeNode root) {
        return check(root, root);
    }

    public boolean check(TreeNode u, TreeNode v) {
        Queue<TreeNode> q = new LinkedList<TreeNode>();
        q.offer(u);
        q.offer(v);
        while (!q.isEmpty()) {
            u = q.poll();
            v = q.poll();
            if (u == null && v == null) {
                continue;
            }
            if ((u == null || v == null) || (u.val != v.val)) {
                return false;
            }

            q.offer(u.left);
            q.offer(v.right);

            q.offer(u.right);
            q.offer(v.left);
        }
        return true;
    }
}
```

