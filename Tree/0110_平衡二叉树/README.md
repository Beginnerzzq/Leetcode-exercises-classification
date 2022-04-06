# 0110_平衡二叉树

##   题目信息

[题目信息](https://leetcode-cn.com/problems/balanced-binary-tree/)

给定一个二叉树，判断它是否是高度平衡的二叉树。

本题中，一棵高度平衡二叉树定义为：

> 一个二叉树*每个节点* 的左右两个子树的高度差的绝对值不超过 1 。

##   思路与题解

### 		    我的思路

* **自顶向下递归**

  我的递归存在缺陷。时间有点长了

  执行用时：1 ms, 在所有 Java 提交中击败了48.87%的用户

  时间复杂度：O(n^2)O(n^2)，其中 nn 是二叉树中的节点个数。
  最坏情况下，二叉树是满二叉树，需要遍历二叉树中的所有节点，时间复杂度是 O(n)O(n)。
  对于节点 pp，如果它的高度是 dd，则 \texttt{height}(p)height(p) 最多会被调用 dd 次（即遍历到它的每一个祖先节点时）。对于平均的情况，一棵树的高度 hh 满足 O(h)=O(\log n)O(h)=O(logn)，因为 d \leq hd≤h，所以总时间复杂度为*O*(*n*log*n*)。对于最坏的情况，二叉树形成链式结构，高度为 O(n)*O*(*n*)，此时总时间复杂度为 O(n^2)*O*(*n*2)。

###     别人的题解

* **自底向上递归**

  中序遍历把二叉树转变为有序数组，然后在根据有序数组构造平衡二叉搜索树。

  时间复杂度：O(n)O(n)，其中 nn 是二叉树中的节点个数。使用自底向上的递归，每个节点的计算高度和判断是否平衡都只需要处理一次，最坏情况下需要遍历二叉树中的所有节点，因此时间复杂度是 O(n)O(n)。


##   源码

* 自顶向下递归

```java
class Solution {
    public boolean isBalanced(TreeNode root) {
        if(root == null){
            return true;
        }
        if(height(root.left) - height(root.right) > 1){
            return false;
        }

        if(height(root.right) - height(root.left) > 1){
            return false;
        }

        if(isBalanced(root.left)){
            return isBalanced(root.right);
        }
        return false;
    }

    // 返回 以该结点为根结点的树的高度
	private int height(TreeNode node) {
        if(node == null){
            return 0;
        }
		return Math.max(
            node.left == null ? 0 : height(node.left), node.right == null ? 0 : height(node.right)
        ) + 1;
	}
}
```

* 自底向上递归

```java
class Solution {
    public boolean isBalanced(TreeNode root) {
        return height(root) >= 0;
    }

    public int height(TreeNode root) {
        if (root == null) {
            return 0;
        }
        int leftHeight = height(root.left);
        int rightHeight = height(root.right);
        if (leftHeight == -1 || rightHeight == -1 || Math.abs(leftHeight - rightHeight) > 1) {
            return -1;
        } else {
            return Math.max(leftHeight, rightHeight) + 1;
        }
    }
}
```

