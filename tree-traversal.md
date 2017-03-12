# Tree Traversal

* Preorder

using stack to print the preorder of the tree iteratively

```java
 public List<Integer> preorderTraversalIte(TreeNode root) {
     List<Integer> ret=new ArrayList<Integer>();
     if(root==null)    
         return ret;
     ArrayDeque<TreeNode> stack=new ArrayDeque<>();
     stack.push(root);
     while(!stack.isEmpty()){
         TreeNode curr=stack.pop();
         ret.add(curr.val);
         if(curr.right!=null) //先push右边
         stack.push(curr.right);
         if(curr.left!=null) //后push左边
         stack.push(curr.left);
     }
     return ret;
 }
```

using  recursive stack to print the preorder

```java
 public void preorderTraversal(TreeNode root,List<Integer> ret) {
         if(root==null)
         return;
         list.add(root);
         preorderTraversal(root.left,ret);
         preorderTraversal(root.right,ret);
 }
```

* Inorder 

using a stack, but difference between using stack to do the preorder, here we push all the left node to stack right away

```java
public List<Integer> inorderTraversal(TreeNode root) {
    List<Integer> list =new ArrayList<>();
    if(root==null)
    return list;

    ArrayDeque<TreeNode> stack=new ArrayDeque<TreeNode>();
    while(root!=null){
    stack.push(root);
    root=root.left;
    }

    while(!stack.isEmpty()){
        TreeNode curr=stack.pop();
        list.add(curr.val);
        TreeNode right=curr.right;
        while(right!=null){
        stack.push(right);
        right=right.left;
        }    
    }
    return list;
}
```

* Postorder

using the same idea as preorder

for a tree like 1\|2,3\|4,5,6   

preorder: 1 \(2 \(4 5\)\)\( 3 \(6\)\) 

postorder is \(\(4 5\) 2\)\(\(6\) 3\) 1 

using  linkedlist, everytime insert in the first

```java
public List<Integer> postorderTraversal(TreeNode root) {
    List<Integer> list =new LinkedList<>();
    if(root==null)
    return list;

    ArrayDeque<TreeNode> stack=new ArrayDeque<>();
    stack.push(root);
   while(!stack.isEmpty()){
       TreeNode curr=stack.pop();
       list.addFirst(curr.val); //preorder添加list尾部，postorder插入list的头部
       if(curr.left!=null) //先push 左边 和preorder是相反的顺序
       stack.push(curr.left);
       if(curr.right!=null) //后push 右边
       stack.push(curr.right);
   }
    return list;
}
```

* Level order

利用Queue

```java
 public List<List<Integer>> levelOrder(TreeNode root) {
         List<List<Integer>> ret=new ArrayList<>();
         if(root==null)
         return ret;

         ArrayDeque<TreeNode> nodeQueue=new ArrayDeque<>();
         nodeQueue.offer(root);
         while(!nodeQueue.isEmpty()){
               int size=nodeQueue.size();
               List<Integer> currLevel=new ArrayList<>();
               for(int i=0;i<size;i++){
                       TreeNode currRoot=nodeQueue.poll();
                       currLevel.add(currRoot.val);
                       if(currRoot.left!=null)
                       nodeQueue.offer(currRoot.left);
                       if(currRoot.right!=null)
                       nodeQueue.offer(currRoot.right);
                 }  
                 ret.add(currLevel);
         }
         return ret;
 }
```

* Binary Tree Vertical Order Traversal



* Zigzag order



