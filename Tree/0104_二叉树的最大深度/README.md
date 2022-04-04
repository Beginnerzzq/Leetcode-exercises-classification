# 0104_二叉树的最大深度

##   题目信息

[题目信息](https://leetcode-cn.com/problems/maximum-depth-of-binary-tree/)

给定一个二叉树，找出其最大深度。

二叉树的深度为根节点到最远叶子节点的最长路径上的节点数。

##   思路与题解

### 		    我的思路

* **递归**

  通过遍历数组计算出每个节点的深度，并把每个节点的深度加入到depths中，然后找出depths中最大的那个，返回。

###     别人的题解

* **递归**

  看看别人的递归，我是真的垃圾。

* **深度优先和广度优先**

##   源码

* 我的递归

```java
class Solution {
    List<Integer> depths = new ArrayList<Integer>();

    public int maxDepth(TreeNode root) {
        if(root == null){
            return 0;
        }
        int depth = 1;
        int res = 1;
        fixOrder(root, depth);
        if(depths.size() != 1){
            for(int i = 0; i < depths.size(); i++){
                // System.out.print(depths.get(i));
                if(depths.get(i) > res){
                    res = depths.get(i);
                    System.out.print(res);
                }
            }
        }

        return res;
    }

    private void fixOrder(TreeNode node, int depth){
        depths.add(depth);
        depth++;
        if(node == null){
            return;
        }
        if(node.left != null){
            fixOrder(node.left,depth);
        }
        if(node.right != null){
            fixOrder(node.right,depth);
        }
    }
}
```

* 递归

```java
class Solution {
    public int maxDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }
        int left = maxDepth(root.left);
        int right = maxDepth(root.right);
        return Math.max(left, right) + 1;
    }
}
```

