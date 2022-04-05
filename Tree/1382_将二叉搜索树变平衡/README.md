# 1382_将二叉搜索树变平衡

##   题目信息

[题目信息](https://leetcode-cn.com/problems/balance-a-binary-search-tree/)

给你一棵二叉搜索树，请你返回一棵 平衡后 的二叉搜索树，新生成的树应该与原来的树有着相同的节点值。如果有多种构造方法，请你返回任意一种。

如果一棵二叉搜索树中，每个节点的两棵子树高度差不超过 1 ，我们就称这棵二叉搜索树是 平衡的 。

##   思路与题解

### 		    我的思路

* **旋转（个人认为，这才是这道题要考的，别人的题解里几乎找不到旋转手撕的方法）**

  思路很清晰，通过旋转的方式降低高度，详情见注释。

  手写if判断，是否需要旋转。这道题与我之前学过的旋转方法不同的是，当一个子树高度过高时，我的代码需要判断多次且旋转多次才能得到正确答案，而这个多次取决于leetcode的用例到底有多深。

  例如用例：`[14,1,15,null,7,null,17,2,12,null,null,null,3,9,null,null,null,null,11]`

  当我想用递归来解决时，发现很难。这个问题留待以后解决。目前靠自己还是没有做出来。

###     别人的题解

* **树转数组，数组转树**

  中序遍历把二叉树转变为有序数组，然后在根据有序数组构造平衡二叉搜索树。

##   源码

* 旋转

```java
class Solution {
    public TreeNode balanceBST(TreeNode root) {
        if(root == null){
            return null;
        }
        if(height(root.left) - height(root.right) > 1){
            //如果它的左子树的右子树高度大于它的左子树的高度
			if(root.left != null && height(root.left.right) > height(root.left.left)) {
				//先对当前结点的左结点(左子树)->左旋转
				leftRotate(root.left);
				//再对当前结点进行右旋转
				rightRotate(root);
			} else {
				//直接进行右旋转即可
				rightRotate(root);
			}
        }

        if(height(root.right) - height(root.left) > 1){
            //如果它的右子树的左子树的高度大于它的右子树的右子树的高度
			if(root.right != null && height(root.right.left) > height(root.right.right)) {
				//先对右子结点进行右旋转
				rightRotate(root.right);
				//然后在对当前结点进行左旋转
				leftRotate(root); //左旋转..
			} else {
				//直接进行左旋转即可
				leftRotate(root);
			}
        }

        return root;
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

    //左旋转
    private void leftRotate(TreeNode root){
        //创建一个与根节点值相同的新节点
        TreeNode newNode = new TreeNode(root.val);
        //把新的结点的左子树设置成当前结点的左子树
        newNode.left = root.left;
        //把新的结点的右子树设置成当前结点的右子树的左子树
        newNode.right = root.right.left;
        //把当前结点的值替换成右子结点的值
        root.val = root.right.val;
        //把当前结点的右子树设置成当前结点右子树的右子树
        root.right = root.right.right;
        //把当前结点的左子树(左子结点)设置成新的结点
        root.left = newNode;
    }

    //右旋转
    private void rightRotate(TreeNode root){
        //创建一个与根节点值相同的新节点
        TreeNode newNode = new TreeNode(root.val);
        //把新的结点的右子树设置成当前结点的右子树
        newNode.right = root.right;
        //把新的结点的左子树设置成当前结点的左子树的右子树
        newNode.left = root.left.right;
        //把当前结点的值替换成左子结点的值
        root.val = root.left.val;
        //把当前结点的左子树设置成当前结点左子树的左子树
        root.left = root.left.left;
        //把当前结点的右子树(右子结点)设置成新的结点
        root.right = newNode;
    }
}
```

* 树转数组，数组转树

```java
class Solution {
    ArrayList <Integer> res = new ArrayList<Integer>();
    // 有序树转成有序数组
    private void travesal(TreeNode cur) {
            if (cur == null) return;
            travesal(cur.left);
            res.add(cur.val);
            travesal(cur.right);
        }
    // 有序数组转成平衡二叉树
    private TreeNode getTree(ArrayList <Integer> nums, int left, int right) {
        if (left > right) return null;
        int mid = left + (right - left) / 2;
        TreeNode root = new TreeNode(nums.get(mid));
        root.left = getTree(nums, left, mid - 1);
        root.right = getTree(nums, mid + 1, right);
        return root;
    }
    public TreeNode balanceBST(TreeNode root) {
        travesal(root);
        return getTree(res, 0, res.size() - 1);
    }
}
```

* 一位手撕AVL树的大佬的代码，利用缓存储存高度求解，我还没看懂

```java
class Solution {
    public TreeNode balanceBST(TreeNode root) {
        if (root == null){
            return null;
        }
        // node节点的高度缓存
        Map<TreeNode,Integer> nodeHeight = new HashMap<>();
        TreeNode newRoot = null;
        Deque<TreeNode> stack = new LinkedList<>();
        TreeNode node = root;
        // 先序遍历插入（其实用哪个遍历都行）
        while(node != null || !stack.isEmpty()){
            if (node != null){
                // 新树插入
                newRoot = insert(newRoot,node.val,nodeHeight);
                stack.push(node);
                node = node.left;
            }else {
                node = stack.pop();
                node = node.right;
            }
        }
        return newRoot;
    }

    /**
     * 新节点插入
     * @param root root
     * @param val 新加入的值
     * @param nodeHeight 节点高度缓存
     * @return 新的root节点
     */
    private TreeNode insert(TreeNode root,int val,Map<TreeNode,Integer> nodeHeight){
        if (root == null){
            root = new TreeNode(val);
            nodeHeight.put(root,1);// 新节点的高度
            return root;
        }
        TreeNode node = root;
        int cmp = val - node.val;
        if (cmp < 0){
            // 左子树插入
            node.left = insert(root.left,val,nodeHeight);
            // 如果左右子树高度差超过1，进行旋转调整
            if (nodeHeight.getOrDefault(node.left,0) - nodeHeight.getOrDefault(node.right,0) > 1){
                if (val > node.left.val){
                    // 插入在左孩子右边，左孩子先左旋
                    node.left = rotateLeft(node.left,nodeHeight);
                }
                // 节点右旋
                node = rotateRight(node,nodeHeight);
            }
        }else if (cmp > 0){
            // 右子树插入
            node.right = insert(root.right,val,nodeHeight);
            // 如果左右子树高度差超过1，进行旋转调整
            if (nodeHeight.getOrDefault(node.right,0) - nodeHeight.getOrDefault(node.left,0) > 1){
                if (val < node.right.val){
                    // 插入在右孩子左边，右孩子先右旋
                    node.right = rotateRight(node.right,nodeHeight);
                }
                // 节点左旋
                node = rotateLeft(node,nodeHeight);
            }
        }else {
            // 一样的节点，啥都没发生
            return node;
        }
        // 获取当前节点新高度
        int height =  getCurNodeNewHeight(node,nodeHeight);
        // 更新当前节点高度
        nodeHeight.put(node,height);
        return node;
    }

    /**
     * node节点左旋
     * @param node node
     * @param nodeHeight node高度缓存
     * @return 旋转后的当前节点
     */
    private TreeNode rotateLeft(TreeNode node,Map<TreeNode,Integer> nodeHeight){
        // ---指针调整
        TreeNode right = node.right;
        node.right = right.left;
        right.left = node;
        // ---高度更新
        // 先更新node节点的高度，这个时候node是right节点的左孩子
        int newNodeHeight = getCurNodeNewHeight(node,nodeHeight);
        // 更新node节点高度
        nodeHeight.put(node,newNodeHeight);
        // newNodeHeight是现在right节点左子树高度，原理一样，取现在right左右子树最大高度+1
        int newRightHeight = Math.max(newNodeHeight,nodeHeight.getOrDefault(right.right,0)) + 1;
        // 更新原right节点高度
        nodeHeight.put(right,newRightHeight);
        return right;
    }

    /**
     * node节点右旋
     * @param node node
     * @param nodeHeight node高度缓存
     * @return 旋转后的当前节点
     */
    private TreeNode rotateRight(TreeNode node,Map<TreeNode,Integer> nodeHeight){
        // ---指针调整
        TreeNode left = node.left;
        node.left = left.right;
        left.right = node;
        // ---高度更新
        // 先更新node节点的高度，这个时候node是right节点的左孩子
        int newNodeHeight = getCurNodeNewHeight(node,nodeHeight);
        // 更新node节点高度
        nodeHeight.put(node,newNodeHeight);
        // newNodeHeight是现在left节点右子树高度，原理一样，取现在right左右子树最大高度+1
        int newLeftHeight = Math.max(newNodeHeight,nodeHeight.getOrDefault(left.left,0)) + 1;
        // 更新原left节点高度
        nodeHeight.put(left,newLeftHeight);
        return left;
    }

    /**
     * 获取当前节点的新高度
     * @param node node
     * @param nodeHeight node高度缓存
     * @return 当前node的新高度
     */
    private int getCurNodeNewHeight(TreeNode node,Map<TreeNode,Integer> nodeHeight){
        // node节点的高度，为现在node左右子树最大高度+1
        return Math.max(nodeHeight.getOrDefault(node.left,0),nodeHeight.getOrDefault(node.right,0)) + 1;
    }
}
```

