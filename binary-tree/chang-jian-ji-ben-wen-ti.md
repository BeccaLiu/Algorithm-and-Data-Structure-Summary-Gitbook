A binary tree is a tree data structure in which** each node has at most**_** two children**_, which are referred to as the left child and the

right child

* 求节点个数

```java
int getNodeCountRec(TreeNode root){
    if(root==null)
    return 0;
    return getNodeCount(root.left)+getNodeCount(root.right);
}

int getNodeCountIte(TreeNode root){
    ArrayDeque<TreeNode> queue=new ArrayDeque<>();
    queue.offer(root);
    int size=0;
    while(!queue.isEmpty()){
        TreeNode curr=queue.poll();
        size++;
        if(curr.left!=null)
        queue.offer(curr.left);
        if(curr.right!=null)
        queue.offer(curr.right);
    }
    return size;
}
```

* 求深度

```java
int getDepthRec(TreeNode root){
    if(root==null)
    return 0;
    return Math.max(getDepthRec(root.left),getDepthRec(root.right))+1;
}

int getDepthIte(TreeNode root){
    ArrayDeque<TreeNode> queue=new ArrayDeque<>();
    queue.offer(root);
    int depth=0;
    while(!queue.isEmpty()){
        int size=queue.size();
        for(int i=0;i<size;i++){
            TreeNode curr=queue.poll();
            if(curr.left!=null)
            queue.offer(curr.left);
            if(curr.right!=null)
            queue.offer(curr.right);
        }
        depth++;
    }
    return depth;
}
```

* 前序遍历，中序遍历，后续遍历

```java
void preOrder(TreeNode root, ArrayList<Integer> list){
    if(root==null)
    return;
    list.add(root.val);
    preOrder(root.left);
    preOrder(root.right);
}
```

* 层序遍历

* 二叉树-&gt;双向有序链表

题目要求：将二叉查找树转换成排序的双向链表\(中序遍历链表\)，不能创建新节点，只调整指针。查找树的结点定义如下：既然是树，其定义本身就是递归的，自然用递归算法处理就很容易。将根结点的左子树和右子树转换为有序的双向链表，然后根节点的left指针指向左子树结果的最后一个结点，同时左子树最后一个结点的right指针指向根节点；根节点的right指针指向右子树结果的第一个结点同时右子树第一个结点的left指针指向根节点。

Given a binary tree, flatten it to a linked list in-place.

```java
TreeNode[] covertBST2DDLRec(TreeNode root){
    if(root==null)
    return new TreeNode[]{root,root};

    TreeNode[] rt=new TreeNode[2]{null,null};

    if(root.left!=null){
        TreeNode[] left=covertBST2DDLRec(root.left);
        left[1].right=root;
        root.left=left[1];
        rt[0]=left[0];
    } 
    else
        rt[0]=root; 

    if(root.right!=null){
        TreeNode[] right=covertBST2DDLRec(root.right);
        right[0].left=root;
        rt[1]=right[1];
    }  
    else
        rt[1]=root;

    return rt;
}
```

注意和总结：1.利用返回一个TreeNode array存的是子问题的头和尾。

Iterative的思路,和preorder traversal的思路是一样的，不过每次弹出一个treeNode时要多做一些处理

```java
TreeNode covertBST2DDLIte(TreeNode root){
    ArrayDeque<TreeNode> stack=new ArrayDeque<TreeNode>();
    while(root!=null){
        stack.push(root);
        root=root.left;
    }

    TreeNode rt=stack.peek();
    TreeNode pre=null;

    while(!stack.isEmpty()){
        TreeNode curr=stack.pop();
        if(pre!=null){ //取值转向
            pre.right=curr;
            curr.left=pre;
        }
        pre=curr;

        curr=curr.right;
        while(curr!=null){
            stack.push(curr);
            curr=curr.left;
        }
    }
    return rt;
}
```

注意事项：1. 压入stack中的每个treeNode, 都不用关心treeNode.left的指针，因为所有treeNode.left要么为空，要么依旧保存入stack 中。2. 需要一个pre来记录每一次的前驱treenode

* 二叉树叶子节点的个数

```java
int countLevelRec(TreeNode root){
        if(root==null)
        return 0;
        if(root.left==null&&root.right==null)
        return 1;

        return countLevelRec(root.left)+countLevelRec(root.right);
}

int countLevelIte(TreeNode root){
        ArrayDeque<TreeNode> queue=new ArrayDeqye<>();
        queue.push(root);
        int count=0;
        while(!queue.isEmpty()){
                TreeNode curr=queue.poll();
                if(curr.left==null&&curr.right==null)
                   count++;
                if(curr.left!=null)
                        queue.offer(curr.left);
                if(curr.right!=null)
                        queue.offer(curr.right);    
        }
        return count;
}
```

* 是否对称树 

```java
public boolean isSymmetric(TreeNode root) {
        if(root==null)
        return true;
        else return ite(root.left,root.right);

}

public boolean isSymmetricHelper(TreeNode left, TreeNode right){
        if(left==null&&right==null)
        return true;
        else if(left==null||right==null)
        return false;
        return left.val==right.val&&isSymmetricHelper(left.left,right,right)&&isSymmetricHelper(left.right,right.left);
}
```

* 是否BST

```java
public boolean isBST(TreeNode root) {
    return isBSTHelper(root,Integer.MIN_VALUE,Integer.MAX_VALUE);
}

public boolean isBSTHelper(TreeNode root,int min,int max){
    if(root==null)
    return true;
    return root.val>min&&root.val<max&&isBSTHelper(root.left,min,root.val)&&isBSTHelper(root.right,root.val,max);

}
```

* 是否AVL 平衡二叉树

AVL：In an AVL tree, the heights of the two child subtrees of any node differ by at most one

```java
public boolean isAVL(TreeNode root){
return isAVLHelper(root)==Integer.MAX_VALUE?false:true;
}

public int isAVLHelper(TreeNode root){
    if(root==null)
    return 0;
    int left=isAVLHelper(root.left);
    int right=isAVLHelper(root.right);
    if(left==Integer.MAX_VALUE||right==Integer.MAX_VALUE)
    return Integer.MAX_VALUE;
    else if(Math.abs(left-right)<=1)
    return Math.max(left,right)+1;
}
```

* 是否Complete BST

In a complete binary tree every level, except possibly the last, is completely filled, and all nodes in the last level are as far left as possible. It can have between 1 and 2h nodes inclusive at the last level h.

```java
boolean isCompleteBSTIte(TreeNode root){
    ArrayDeque<TreeNode> q=new ArrayDeque<>();
    q.offer(root);
    isEnd=true;
    while(!q.isEmpty()){
            TreeNode curr=q.poll();
            if(curr.left!=null){
            if(isEnd)
            return false;
            curr.offer(curr.left);
            }
            else
            isEnd=true;

            if(curr.right!=null){
            if(isEnd)
            return false
            curr.offer(curr.left);
            }
            else
            isEnd=true;
    }
        return true;
}
```

* Lowest Common Ancestor of a Binary Search Tree

According to the definition of LCA on Wikipedia: “The lowest common ancestor is defined between two nodes v and w as the lowest node in T that has both v and w as descendants \(where we allow a node to be a descendant of itself\).”

分析:如果是BST，这道题会非常简单，BST的特征是，左边的孩子都小，右边的孩子都大，所以每一次递归，对于一个root节点，p,q要么都小于等于root，要么都大与等于root，（这两种情况，我们继续进入下一层递归）要么一个左，一个右，这说明p，q分开了，此时root则为ancestor。

```java
public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
    if(root==null)
    return null;

    if(p.val==root.val||q.val==root.val||(p.val<root.val&&q.val>root.val||q.val<root.val&&p.val>root.val))
    return root;
    else if(p.val<root.val&&q.val<root.val)
    return lowestCommonAncestor(root.left,p,q);
    else
    return lowestCommonAncestor(root.right,p,q);
}

public TreeNode lowestCommonAncestorIte(TreeNode root, TreeNode p, TreeNode q){
    if(p.val==q.val)
    return p;
    while(root.val!=p.val||root.val!=q.val){
        if(p.val<root.val&&q.val<root.val)
        root=root.left;
        else if (p.val>root.val&&q.val>root.val)
        root=root.right;
        else
        return root;
     } 
    return root;
}
```

* Construct Binary Tree from Preorder and Inorder Traversal

* Construct Binary Tree from Inorder and Postorder Traversal

* Delete a node from BST



