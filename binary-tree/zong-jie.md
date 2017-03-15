Tree的题目一般两种解法, 一种top down, 一种bottom up, bottom up的做法占了70%

top down：进入递归时，往递归中传入一些关于父节点的信息，处理一些信息，然后再进入递归，一般到了底，就把结果直接返回，这种写法也比较容易转换成iterative

模版：

```java
returnValue dfsHelper(TreeNode root, InformationFromParent){
//base case
if(root==null)
return returnValue;

//process InformationFromParent 
return dfsHelper(root, InformationAfterProcess);
}
```

bottom up, 先走到leaves, 然后决定要往上一层传什么值，一般情况dfsHelper返回的会是题目要求的值，复杂的情况，可能要穿比题目更多的信息。过程先分析base case，再挑任意的一个node，分析应该往上层传什么值。

模版：

```java
returnInformatioin（有时local信息的数组） dfsHelper(TreeNode root, 有时侯会在这放一个global的数组，用来存结果)｛
//base case
if(root==null)
return Information

Info left=dfsHelper(root,left....);
Info right=dfsHelper(root.right...);
//process Info
//有时需要update global的信息
return Info after process
｝
```

这里具体分析下Bottom up:

* 题一：给一个普通的tree，找LCA

分析：

1. intutive idea：对于每一个node, 去左子树看有没找到p，q,右子数找没找到p,q通过返回的找到p，q的个数来判断

time：第一次看n个点，第二次根据情况，去掉一半的可能性，看n/2个点，总共复杂度为n+n/2+n/4.....1=F\(n\)

> 数学推导：2F\(n\)=2n+n+n/2+n/4+....2,  2F\(n\)-F\(n\)=2n＋2=F\(n\), 所以F\(n\)=2n+2

但是有个陷阱，以上复杂度计算是基于树是平衡的，如果树是像list一样的结构，则worst case 为O\(n^2\)  \(n+n-1+n-2+....2\)=

```java
public TreeNode findLCAIte(TreeNode root, TreeNode p, TreeNode q){
    if(root==null)
    return root;
    if(p==q)
    return p;
    while(root!=null){
        int left=findNodeDfs(root.left,p,q);
        int right=findNodeDfs(root.right,p,q);
        if(left==1&&right==1||(root==p||root==q)&&left+right==1)
        return root;
        if(left==2)
        root=root.left;
        else if(right==2)  
        root=root.right;      
    }
    return root;
}

public int findNodeDfs(TreeNode root, TreeNode p, TreeNode q){
    if(root==null)
    return 0;
    int count=root==p||root==q?1:0;
    return count+findNodeDfs(root.left,p,q)+findNodeDfs(root.right,p,q);
}
```

2.改进使用Bottom Up DFS，这里要注意一个细节，那就是否p,q 一定存在在给的tree中

思路：

方法一：先从最基本的开始分析，题目要求返回treeNode，这里初始化也假定返回treeNode，如果数据信息不足，再做打算。经过分析对于任意一个节点有以下三情况

a.左边返回一个treeNode，右边返回一个treeNode

b.左边返回TreeNode，右边返回Null

c.左边返回null，右边返回TreeNode

d.左右都返回null

情况a：左边找到了一个点，右边找到了一个点，说明现在这个点是ancestor，return itself

情况b/c：一边返回TreeNode，另一边返回空。返回TreeNode的那边有可能是返回的ancestor，有可能是input p或input q，这里先尝试性的返回传上来的点。

情况d：返回null

通过返回一个节点或者返回null节点的区别来判断

follow up: p和q不一定存在，差别在于，如果返回道findLCAIte的值是p或是q，究竟是ancesor是p和q还是，有个node压根没找到，对于这个问题，我们需要多余的信息，比如一个boolean\[\] find=new boolean\[2\]来代表是否好到p和q

```java
public TreeNode findLCAIte(TreeNode root, TreeNode p, TreeNode q){
    if(root==null)
    return null;
    if(p==q)
    return p;

    boolean[] found=new boolean[2];
    TreeNode rt= findLCAHelper(root,p,q，found);
    //针对follow up
    return found[0]&&found[1]?return rt:return null;  
｝

public TreeNode findLCAHelper(TreeNode root, TreeNode p, TreeNode q,boolean[] isFound){
    if(root==null)
    return null;

    TreeNode left=findLCAHelper(root.left,p,q);
    TreeNode right=findLCAHelper(root.right,p,q);
    if(left!=null&&right!=null||(root==p||root==q)){
    //针对follow up, 在找到p，q时更新对应的isFound
    if(isFound[0]==false&&root==p)
    isFound[0]=true;
    if(isFound[1]==false&&root==q)
    isFound[1]=true;
    return root;
    }
    else if(left==null&&right!=null)
    return right;
    if(left!=null&&right==null)
    return left;
    else 
    return null;
}
```

方法二：通过设置最直观的返回值boolean代表是否找到对应的节点，把结果存在一个全局的变量ancestor中

```java
 public static boolean lowestCommonAncestor236(TreeNode root, TreeNode p, TreeNode q, TreeNode[] ancestor) {
        if(root==null)
            return false;
        boolean findAtLeft=lowestCommonAncestor236(root.left,p,q,ancestor);
        boolean findAtRight=lowestCommonAncestor236(root.right,p,q,ancestor);
        if((findAtLeft&&findAtRight&&ancestor[0]==null)||(root==p||root==q)&&(findAtLeft||findAtRight)){//left has exist and right has exist and ancestor never be updated before
            ancestor[0]=root;
        }
        return findAtLeft||findAtRight||root==p||root==q; //check if we found root;
}
```

Follow-up 如果给一个TreeNode List,找全部treeNode的ancestor

用方法二做follow up

```java
public static int lowestCommonAncestor236(TreeNode root, HashSet<TreeNode> nodes, TreeNode[] ancestor) {
        if(root==null)
            return 0;
        int findAtLeft=lowestCommonAncestor236(root.left,p,q,ancestor);
        int findAtRight=lowestCommonAncestor236(root.right,p,q,ancestor);
        if((ancestor[0]==null&&left+right==nodes.size())||nodes.contains(root)&&(left+right+1==nodes.size())){//left has exist and right has exist and ancestor never be updated before
            ancestor[0]=root;
        }
        return findAtLeft+findAtRight+nodes.contains(root)?1:0; //check if we found root;
}
```

* 题目二：longest distance in Tree（结果不是直接返回，而是存在一个arr的数组中，适时更新）

即二叉树中相距最远的两个叶子节点之间的距离，对于每一层，我既要返回叶子节点到现在点的最大值，又要计算一个全局最大值，所以这里我们把全局最大值放在一个arr中传递下去, 而返回的是局部最大

```java
public int getMaxDistance(TreeNode root,int[] maxLen){
    if(root==null)
    return 0;

    int leftDis=getMaxDistance(root.left);
    int rightDis=getMaxDistance(root.right);
    //update global maxLen
    if(leftDis>0&&rightDis>0&&leftDis+rightDis>maxLen[0])
    maxLen[0]=leftDis+rightDis;

    return Math.max(leftDis,rightDis)+1;
}
```

* 题目三：Largest BST Subtree

```java
 //int[3]: count, min, max 
 //when count=-1 means not a valid BST 
 public int[] largestBSTSubtreeHelper(TreeNode root,int[] maxSize) {
         if(root==null)
         return new int[]{0,Integer.MAX_VALUE,Integer.MIN_VALUE};
         
         int[] left=largestBSTSubtreeHelper(root.left,maxSize);
         int[] right=largestBSTSubtreeHelper(root.right,maxSize);
         
         int[] rt=new int[]{0,Integer.MAX_VALUE,Integer.MIN_VALUE};
         if(left[0]>=0&&root.val>left[2]){
             rt[1]=Math.min(root.val,left[1]);
             rt[0]+=left[0];
         }
         if(right[0]>=0&&root.val<right[1]){
             rt[2]=Math.max(root.val,right[2]);
             rt[0]+=right[0];
         }
         
         if(left[0]>=0&&right[0]>=0&&root.val>left[2]&&root.val<right[1])
         rt[0]+=1;
         else
         rt[0]=-1;
         //System.out.println(Arrays.toString(rt));
         if(rt[0]>maxSize[0])
         maxSize[0]=rt[0];
         return rt;
    }
```



