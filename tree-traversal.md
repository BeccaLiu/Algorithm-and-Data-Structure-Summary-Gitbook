# Tree Traversal

time complexity is usually O\(n\) ,space complexity is usually O\(logn\) the height of the tree

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

* ZigZag level traversal

同上，唯一注意的是

1. 用一个isLeftToRight 的boolean flag，每层traverse完，isLeftToRight=!isLeftToRight
2. if\(isLeftToRight\) list.add\(root.val\)
3. else list.addFirst\(root.val\)

4. Binary Tree Vertical Order Traversal

```java
//DFS: dfsHelper(root,new LinkedList<List<Integer>>,new LinkedList<List<Integer>>,0)
public static void dfsHelper(TreeNode root,List<List<Integer>> left, List<List<Integer>> right, int level){
    if(root==null)
    return;

    //add current root value to correspond list
    if(level>=0){
    if(right.size()==level)
    right.add(new ArrayList<>());
    right.get(level).add(root.val);
    }
    else{
    if(left.size()==-level-1)
    left.add(new ArrayList<>());
    left.get(-level-1).add(root.val);
    ｝
    dfsHelper(root.left, left, right, level-1);
    dfsHelper(root.right, left, right, level+1);
}

//BFS 
一个queue记录node来traversal，用一个queue记录node的对应的level的值，依旧用两个list：leftList和rightList
 public static List<List<Integer>> verticalOrderBFS(TreeNode root) {
     //关键代码

     ArrayDeque<TreeNode> nodeQueue=new ArrayDeque<>(); //正常level traversal的queue
     ArrayDeque<Integer> levelQueue=new ArrayDeque<>();  //专门存对应的level 数，以root 为中心，左边为－1，右边为1
     nodeQueue.offer(root); //initial
     levelQueue.offer(0);

     while(!nodeQueue.isEmpty()){
         TreeNode curr=nodeQueue.poll();
         int level=levelQueue.poll();

         //处理curr node
         if(level>=0)
         //和dfs一样处理，加入rightList
         else
         //和dfs一样,加入leftList

         if(curr.left!=null)｛
         nodeQueue.offer(curr.left);
         levelQueue.offer(level-1);
         ｝
         if(curr.right!=null){
         //同上处理对应的right child node
         }
     }

     //把leftlist reverse，再把rightList append，即为结果
 ｝
```

dfs 方法要注意的细节是，当level&lt;0时，判断的是left.size==-level-1，因为左边的level是从－1开始，可是index是从0开始

时间复杂度两个都是遍历所有节点，空间复杂度，两个都用了两个list来存结果，BFS用了额外的两个queue来便利，DFS用了额外的call stack来便利。

