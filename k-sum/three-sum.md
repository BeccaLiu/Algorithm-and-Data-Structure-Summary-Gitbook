* 3 sum的两种解法：模版

先检查输入：

```
if(nums==null||nums.length<3)
```

1. sort＋two pointer O\(nlogn+n^2\) space O\(1\)

```java
Arrays.sort(nums);
for(int i=0;i<nums.length;i++){
    if(i>0&&nums[i]==nums[i-1]) 
    continue;//查重如有需要
    
    int l=i+1;
    int r=nums.length-1;
    while(l<r){
        if(nums[i]+nums[l]+nums[r]==target){
        //处理数据
        }
        else if(nums[i]+nums[l]+nums[r]<target)
        l++;
        else
        r--;
    }
}
```

1. hashmap + two sum O\(n+n^2\) space O\(n\)

```java
    for(int i=0;i<nums.length-2;i++){
        int target=inputTarget-nums[i];
        HashMap<Integer,Integer> map=new HashMap<>();
            for(int j=i+1;j<nums.length;j++){
                Integer index=map.get(nums[j]);
                if(index!=null){
                      List<Integer> temp=Arrays.asList(new Integer[]{i,index,j});
                      list.add(temp);  
                }
                else
                map.put(target-nums[j],j);
            }
        }

```



* 3sum \(unsorted array+duplicated content\)

Input: unsorted array with duplicated content \[-1,0,1,2,2,-1,-4\]

Output: solution set \[\[-4,2,2\],\[-1,-1,2\],\[-1,0,1\]\] \(unique\)

返回boolean 存在性或返回结果集，不关注index，用sort＋two pointer即可

```java
public List<List<Integer>> threeSum(int[] nums) {
        if(nums==null||nums.length==0)
        return list;

        Arrays.sort(nums);
        for(int i=0;i<nums.length-2;i++){
            if(i>0&&nums[i]==nums[i-1]) //skip duplicated solution
            continue;
            int l=i+1;
            int r=nums.length-1;
            int target=0-nums[i];
            while(l<r){
                if(nums[l]+nums[r]==target){
                List<Integer> temp=Arrays.asList(new Integer[]{nums[i],nums[l],nums[r]});
                list.add(temp);
                l++;r--;
                while(l<r&&nums[l]==nums[l-1]) l++; //skip duplicated solution
                while(l<r&&nums[r]==nums[r+1] r--; 
                 }
                else if(nums[l]+nums[r]<target)
                l++;
                else
                r--;
            }
        }
        return false;     
}
```

注意事项：

1. 把数组变list：Arrays.asList\(new Integer\[\]{1,2,3} 注意这里必须新建的数组是Integer而非int才能转换
2. 因为输入有重复的结果集，通过三个while循环来skip掉重复结果

follow up:返回结果index的组合，则只能用hashmap

```java
public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> list = new ArrayList<>();
        if(nums==null||nums.length==0)
        return list;
        
        for(int i=0;i<nums.length-2;i++){
        int target=-nums[i];
        HashMap<Integer,Integer> map=new HashMap<>();
            for(int j=i+1;j<nums.length;j++){
                Integer index=map.get(nums[j]);
                if(index!=null){
                      List<Integer> temp=Arrays.asList(new Integer[]{i,index,j});
                      list.add(temp);  
                }
                else
                map.put(target-nums[j],j);
            }
        }
        return list;
}
```



* 3Sum Closest

```java
public int threeSumClosest(int[] nums, int target) {

    while(l<r){
        int tempsum=nums[i]+nums[l]+nums[r];
        int diff=Math.abs(target-tempsum);
        if(diff==0){
        return target;
        }
        if(diff<Math.abs(target-sum))
        sum=tempsum;
        
        //每次都在尽力趋近target
        if(tempsum<newTarget)
        l++;
        else
        r--;
    }
｝
```

* 3Sum Smaller

思路：1. 通过i fix第一个number，通过l 来fix第二个number，当i,l,r三者组合&lt;target时，以fix i，fix j和浮动的j总共有r－l个可能性，然后通过l++来计算下一个以fix i，fix l+1, moving r 来看有无新组合

```java
public int threeSumSmaller(int[] nums, int target) {
        if(nums==null||nums.length<3)
        return 0;
        
        Arrays.sort(nums);
        int rt=0;
        for(int i=0;i<nums.length;i++){
            int l=i+1;
            int r=nums.length-1;
            while(l<r){
                int sum=nums[i]+nums[l]+nums[r];
                if(sum<target){
                    rt+=r-l;
                    l++;
                }
                else
                r--;
            }
        }
        return rt;
    }
```





