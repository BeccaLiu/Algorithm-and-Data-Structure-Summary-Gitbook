## Two Sum

* Two sum （unsorted list ＋ hashmap）

```java
public int[] twoSum(int[] nums, int target) {
    HashMap<Integer,Integer> map=new HashMap<>();
    for(int i=0;i<nums.length;i++){
        if(!map.isEmpty())
            Integer index=map.get(nums[i]);
        if(index==null){
            map.put(target-nums[i],i);        
        }
        else{
        return new int[]{index,i};
        }    
    }
return new int[]{};
｝
```

总结：不要忘记检查 map.isEmpty\(\) 当你要使用map.get\(xx\)的时候

