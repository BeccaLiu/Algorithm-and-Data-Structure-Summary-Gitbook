* Subset

时间 空间为2^n 因为对于nums中的每一个数，有放或不放两种可能性，所以最后是2^N

空间 用了一个arraylist，所以是N

Given a set of distinct integers, nums, return all possible subsets.

方法一：

```
               [] 

     [1]         [2]       [3]
  [1,2] [1,3]   [2,3]
[1,2,3]
```

pos means the at current level, we can put from nums\[pos\] to nums\[nums.length-1\] to list

as every result is valid, we do not need to check if list.size\(\)==pos

```java
 public List<List<Integer>> subsets(int[] nums) {
   List<List<Integer>> list=new ArrayList<>();
   if(nums.length==0)
   return list;
   subSetHelper(nums,new ArrayList<Integer>(),list,0)
   return list;
 }
 public void subSetHelper(int[] nums, ArrayList<Integer> list, List<List<Integer>> ret,int pos){
   //if(list.size()==pos){
     ret.add(new ArrayList<Integer>(list));
   //}
   for(int i=pos;i<nums.length;i++){
     list.add(nums[i]);
     subSetHelper(nums,list,ret,pos+1);
     list.remove(list.size()-1);
   }
 }
```

方法二：

```
                \[\]
            \[1\]       \[\]   放不放1
     \[1,2\] \[1\]    \[2\] \[\] 放不放2
[1,2,3][1,2] [1,3][1] [2,3][2] [3][] 放不放3
```

pos：to add nums\[pos\] or not

```java
public void subSetHelper(int[] nums, ArrayList<Integer> list, List<List<Integer>> ret,int pos){
    if(pos==nums.length)
    ret.add(new ArrayList<Integer>(list));

    //add nums[pos]
    list.add(nums[pos]);
    subSetHelper(nums,list,ret,pos+1);
    list.remove(list.size()-1);

    //not add, just go inside
    subSetHelper(nums, list, ret, post+1);
}
```

Follow up: if the length of nums is so huge, can we solve it recursively,

Ans: we can not, as the depth of the solution tree is n, which means we need N depth of stack to store all the recursive call, which will throw **StackOverflowException**

How to: we can so the previous idea using iterative, which the

```java
public List<List<Integer>> subsets(int[] nums) {
   List<List<Integer>> list=new ArrayList<>();
   if(nums.length==0)
   return list;
   list.add(new ArrayList<Integer>());
   List<List<Integer>> next=new ArrayList<>();
   for(int i=0;i<nums;i++){
      for(List<Integer> temp:list){
      // not add
         next.add(new ArrayList<Integer>(temp));
         //add
         temp.add(nums[i]);
         next.add(new ArrayList<Integer>(temp));
      }
      list=next;
      next=new ArrayList<>();
   }
   return list;

 }
```

has duplicated number

```java
public List<List<Integer>> subsets(int[] nums) {
   List<List<Integer>> list=new ArrayList<>();
   if(nums.length==0)
   return list;
   //as the output is set, we do not care the order, so we can sort here
   Arrays.sort(nums);//nlogn
   subSetHelper(nums,new ArrayList<Integer>(),list,0)
   return list;
 }
 
 //time O(2^n)
 //space O(n)
 public void subSetHelper(int[] nums, ArrayList<Integer> list, List<List<Integer>> ret,int pos){
     //not add anything
     ret.add(list);
   
   //add nums[pos]--nums[end]
   for(int i=pos;i<nums.length;i++){
     if(i>0&&nums[i]==nums[i-1])
     continue;
     list.add(nums[i]);
     subSetHelper(nums,list,ret,pos+1);
     list.remove(list.remove(list.size()-1));
   }
 }
```

Follow up : if only need subset with length=k

for the base case 

```
if(list.size()==k)
ret.add(new ArrayLsit<Integer>(list));
```



