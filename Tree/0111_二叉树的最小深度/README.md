# 0111_二叉树的最小深度

##   题目信息

[题目信息](https://leetcode-cn.com/problems/minimum-depth-of-binary-tree/)

给定一个二叉树，找出其最小深度。

最小深度是从根节点到最近叶子节点的最短路径上的节点数量。

**说明：**叶子节点是指没有子节点的节点。

##   思路与题解

### 		    我的思路

* **递归**

  通过遍历数组计算出每个节点的深度，并把每个节点的深度加入到depths中，然后找出depths中最小的那个，返回。
  
  我的代码是真的垃圾，哈哈。
  
  执行用时：100 ms, 在所有 Java 提交中击败了8.49%的用户

###     别人的题解

* **深度优先**

  首先可以想到使用深度优先搜索的方法，遍历整棵树，记录最小深度。

  对于每一个非叶子节点，我们只需要分别计算其左右子树的最小叶子节点深度。这样就将一个大问题转化为了小问题，可以递归地解决该问题。


##   源码

* 递归

```java
class Solution {
    List<Integer> depths = new ArrayList<Integer>();

    public int minDepth(TreeNode root) {
        if(root == null){
            return 0;
        }
        int depth = 1;
        int res = 0;
        fixOrder(root, depth);
        if(depths.size() != 0){
            for(int i = 0; i < depths.size(); i++){
                System.out.println(depths.get(i));
                if(res == 0){
                    res = depths.get(i);
                }else{
                    if(depths.get(i) < res){
                        res = depths.get(i);
                        // System.out.println(res);
                    }
                }
            }
        }

        return res;
    }

    private void fixOrder(TreeNode node, int depth){
        if(node.left == null && node.right == null){
            depths.add(depth);
            System.out.println(depth);
        }
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

* 深度优先

```java
class Solution {
    public int minDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }

        if (root.left == null && root.right == null) {
            return 1;
        }

        int min_depth = Integer.MAX_VALUE;
        if (root.left != null) {
            min_depth = Math.min(minDepth(root.left), min_depth);
        }
        if (root.right != null) {
            min_depth = Math.min(minDepth(root.right), min_depth);
        }

        return min_depth + 1;
    }
}
```

