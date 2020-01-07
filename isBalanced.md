## 给定一个二叉树，判断它是否是高度平衡的二叉树。

> 本题中，一棵高度平衡二叉树定义为：
一个二叉树每个节点 的左右两个子树的高度差的绝对值不超过1。

* 示例 1:

```
给定二叉树 [3,9,20,null,null,15,7]

    3
   / \
  9  20
    /  \
   15   7
```

* 返回 true 。

* 示例 2:

```
给定二叉树 [1,2,2,3,3,null,null,4,4]

       1
      / \
     2   2
    / \
   3   3
  / \
 4   4
 ```
* 返回 false 。

## 分析
* 使用递归的方式进行判断，就是调用自身
* 对高度的实现

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */

class Solution {
    public boolean isBalanced(TreeNode root) {
        height(root);//使用递归进行处理
        return result;
    }
    boolean result = true;
    int height(TreeNode root){
        if(root==null)
           return 0;
        int left = height(root.left);  //计算左子树的高度
        int right = height(root.right); //计算右字数的高度
        //判断左子树和右子树的高度是否大于1，大于1则不满足返回false.
        //小于1的左子树和右字数则满足平衡二叉树 
        if(Math.abs(left - right) > 1){
            result = false;
        }return Math.max(left,right) + 1;  //返回height高度值
    }
}
```
