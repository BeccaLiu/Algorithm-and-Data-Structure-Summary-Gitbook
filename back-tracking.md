搜索问题主要是针对一列数的全排列 （permutation, subsets, combination）或是对一种游戏 \(sudoku, N-Queens\) 的解决方案， 或是一种实际规则（phone number, IP address）的全组合。其本质是用Brute force对所有满足条件的结果进行尝试，看是否最终结果是否满足。

解决算法：

1. * 递归：基本上采用brute-force，针对每一种条件，一层层递归。
     “在循环中递归”。
   * 排序：根据题目的条件决定是否一开始要对数列进行排序。
   * 去重：如果follow-up问题中，如果给出的数列中有重复数字，如【1， 1， 1， 2， 3】,为保证结果里不重复，就需要去重。往往是在递归中对
     非第一个的重复元素
     跳过。
2. 复杂度：
   * 时间：NP问题，是一个指数级。所有可能组合的数目。
   * 空间：主要是占用了递归栈



backtracking是DP的一种，但是单纯的DP，通过状态转移，解决的是：

1. 最长。。。。最短。。。。最多。。。最少。。。

2. 能不能。。。

3. 总共多少种。。。。

如果要得到具体答案，像是输出所有附和条件的路径。。。就要backtracking来做了。

模版：

**如果你已经找到了解决方案，那么返回成功**

**for\(现在位置可以的所有可能选择）｛**

**选择其中一个方案然后沿着路径前进一步**

**使用递归的方法从新的位置解决问题**

**如果新的位置可以成功解决，向上一级返回成功**

**从现在位置恢复到循环之前的位置 ｝**

**如果到这里表示仍然没有成功，返回失败**

排列：排列其实是一个挑选的思想（结果顺序不一，则不相同，所有会用到isVisited的数组）

以\[1, 2, 3\] 为例，排列其实是一个挑选的思想

第一个元素，我可以挑选1，2， 3

第二个元素，如果2被选择了，我只能从1，3中选。

第三个元素，现在只有一个元素还没被选择，只能选这个数了。

我们可以用一个isUsed数组来标记元素是否被选择。

```java
private void doPermute(int[] nums, boolean[] isUsed, List<Integer> store, List<List<Integer>> result) {  
    if (store.size() == nums.length) {  
        result.add(new ArrayList<>(store));  
        return;  
    }  
    for (int i = 0; i < nums.length; i++) {  
        if (!isUsed[i]) {  
            store.add(nums[i]);  
            isUsed[i] = true;  
            doPermute(nums, isUsed, store, result);  
            store.remove(store.size() - 1);  
            isUsed[i] = false;  

        }  
    }  
}
```

组合：

比如subset：每个数字有两种可能性，一个是放，一个是不放，

以数组\[1, 2, 3, 4\]为例。

我们想要2个数的组合，可以选择1, 2, 3, 4。

之后，1可以选择2，3，4；2可以选择3，4；3可以选择4，4没有别的可以选择了。

这里通过限制后面的 index &gt; 前面的index，来控制不出现\[1, 3\] \[3, 1\]这样的。 因为set中\[1,3\],\[3,1\]是一样的

```java
private void doCombine(List<List<Integer>> result, List<Integer> curList, int index, int n, int k) {  
    if (curList.size() == k) {  
        result.add(new ArrayList<>(curList));  
        return;  
    }  
    for (int i = index; i < n; i++) {  
        curList.add(i + 1);  
        doCombine(result, curList, i + 1, n, k);  
        curList.remove(curList.size() - 1);  
    }  
}
```

总结：

注意下一阶段递归结束回上来的时候，要恢复现场！（比如之前设置isUsed = true了，递归结束后应该重置isUsed = false ）。

Ref：

1.[http://buptjz.github.io/2014/02/23/permuteAndBacktrack](http://buptjz.github.io/2014/02/23/permuteAndBacktrack)

2.[http://www.cnblogs.com/zmyvszk/p/5271822.html](http://www.cnblogs.com/zmyvszk/p/5271822.html)

3.[http://kekecv.com/2016/06/17/排列组合问题的回溯\(Backtracking\) 思想总结/](http://kekecv.com/2016/06/17/排列组合问题的回溯%28Backtracking%29 思想总结/)

