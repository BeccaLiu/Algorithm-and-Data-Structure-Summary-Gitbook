Permutations

1. all distinct number

space: n\*\(n-1\)\*\(n-2\)\*....1=n! \(the last level of solution tree is the result list\) and each list is of size n, so the totoal size of List&lt;List&lt;Integer&gt;&gt; will be n!\*n

time: 1+

```java
public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> res=new ArrayList<List<Integer>>();
        if(nums==null||nums.length==0)
        return res;

        permuteHelper(nums,new ArrayList<Integer>(),res,new boolean[nums.length]);
        return res;
    }

public void permuteHelper(int[] nums,ArrayList<Integer> list,List<List<Integer>> ret,boolean[] visited){
        if(list==nums.length){
        ret.add(new ArrayList<Integer>(list));
        return;
        }

        for(int i=0;i<nums.length;i++){
                if(!visited[i]){
                list.add(nums[i]);
                visited[i]=true;
                permuteHelper(nums,list,ret,visited);
                visited[i]=false;
                list.remove(list.size()-1);
                }
        }
}
```



2.if contains duplicate number

```java
Arrays.sort(nums)
if(visited)
```



