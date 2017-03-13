## Two Sum

* Two sum （unsorted list ＋ hashmap） time O\(n\) spaceO\(n\)

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



* Two Sum II - Input array is sorted time \(sorted list + two pointer \)O\(n\) space O\(1\)

```java
public int[] twoSum(int[] numbers, int target) {
    int l=0;
    int r=numbers.length-1;
    while(l<r){
        if(nums[l]+nums[r]==target)
        return new int[]{l+1,r+1};
        else if(nums[l]+nums[r]<target)
        l++;
        else
        r--;
    }
    return new int[]{};
}
```



* Two Sum III - Data structure design

一般设计数据结构或API的题目，开始涉及前要考虑api的频率，怎么降低总体时间复杂度，比如如果下面这个API，add比较频繁，则要保证add处理尽可能快，把一些job放到find中做，当然这个就看需求了

思路 ：

1. 每次find的target不一样，所以不能像之前two sum一样，每次在hashmap中存target-nums\[i\]的做法。
2. 所以我们依旧要一一遍历存好的数据结构，如果这个数据结构时list，这样遍历的时间复杂度还是N^2，如果想加快，则需要额外的数据结构，这里我们依旧会用到hashmap。
3. 接下来思考hashmap中具体存的内容，注意一个特例，比如1，1，2，find\(2\) 要返回true，所以key是数字1，但value不能只是index，不然读到第二个1时，index就被覆盖了，我们应该存frequency，因为题目只要求返回boolean并未要求返回index

```java
public class TwoSum {
    ArrayList<Integer> list; //just append number 
    HashMap<Integer,Integer> map; //number and frequency of number

    /** Initialize your data structure here. */
    public TwoSum() {
        list=new ArrayList<Integer>();
        map=new HashMap<>();
    }
    
    /** Add the number to an internal data structure.. */
    public void add(int number) {
        list.add(number);
        map.put(number,map.getOrDefault(number,0)+1);
    }
    
    /** Find if there exists any pair of numbers which sum is equal to the value. */
    public boolean find(int value) {
        for(int i=0;i<list.size();i++){
            int other=value-list.get(i);
            Integer freq=map.get(other);
            if(freq!=null&&(other!=list.get(i)||freq>1))
                return true;
        }
        return false;
    }
}
```

注意事项：还是上面那个特例：判断返回true的条件是freq!=null&&\(other!=list.get\(i\)\|\|freq&gt;1\) 

follow  up: 如果要求返回index，答value的位置存index的hashset



