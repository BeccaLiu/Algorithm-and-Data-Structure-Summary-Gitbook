# Tree Traversal

1. Inorder
2. 






1. 2. Preorder

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
 public List<Integer> preorderTraversal(TreeNode root,List<>) {
 
 }
```

1. Postorder
2. Level order

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

1. Zigzag order



