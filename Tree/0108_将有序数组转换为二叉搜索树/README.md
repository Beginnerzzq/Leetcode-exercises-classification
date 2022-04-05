# 0108_将有序数组转换为二叉搜索树

##   题目信息

[题目信息](https://leetcode-cn.com/problems/convert-sorted-array-to-binary-search-tree/)

给你一个整数数组 nums ，其中元素已经按 升序 排列，请你将其转换为一棵 高度平衡 二叉搜索树。

高度平衡 二叉树是一棵满足「每个节点的左右两个子树的高度差的绝对值不超过 1 」的二叉树。

##   思路与题解

### 		    我的思路

* **创建BST，再旋转为AVL树**

  这道题的本意是创建一个平衡二叉树（AVL树），我的想法是先创建一个BST树，再判断这棵树应该如何旋转。

  实现起来需要很多的方法，这里就不写了。具体参考[q1382_将二叉搜索树变平衡](./Tree/1382_将二叉搜索树变平衡/README.md)

###     别人的题解

* **取中位数为根节点**

  看看别人的递归，我是真的垃圾。

##   源码

* 取中位数为根节点

```java
class Solution {
    public TreeNode sortedArrayToBST(int[] nums) {
        return helper(nums, 0, nums.length - 1);
    }

    public TreeNode helper(int[] nums, int left, int right) {
        if (left > right) {
            return null;
        }

        // 总是选择中间位置右边的数字作为根节点
        int mid = (left + right + 1) / 2;

        TreeNode root = new TreeNode(nums[mid]);
        root.left = helper(nums, left, mid - 1);
        root.right = helper(nums, mid + 1, right);
        return root;
    }
}
```

