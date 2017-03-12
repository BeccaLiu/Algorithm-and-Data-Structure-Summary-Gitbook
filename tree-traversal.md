# Tree Traversal

1. Inorder



1. Preorder

using stack

```java
 public List<Integer> preorderTraversal(TreeNode root) {
 List<Integer> ret=new ArrayList<Integer>();
 if(root==null)
 
 
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
         
         ArrayDeque<Integer> nodeQueue=new ArrayDeque<Integer>();
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



