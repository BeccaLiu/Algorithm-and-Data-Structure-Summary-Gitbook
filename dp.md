　What is DP?

1.Breaking down a problem into sub-problems.

Bottom-up: where we start from the base cases and compute the values until we reach the desired value

Top-Down: recursive with memorization

01 knapsack

2D array:  row as item number, column as capacity

each cell represent for capacity at column, what is the** value **of each item

初始情况一：对于第0列，它的含义是背包的Capacity为0。此时物品的价值呢？什么都放不进。因此，第一列都填入0。

初始情况二：对于第0行，它的含义是屋内没有物品。那么没有任何物品的背包里的价值多少呢？还是没有！所有都是0。

```
Knapsack Max weight : W = 10 (units) 
Total items         : N = 4
Values of items     : v[] = {10, 40, 30, 50} 
Weight of items     : w[] = {5, 4, 6, 3}
```

![](/assets/import.png)F\(N, C\) = max\(F\(N-1, C-W\[N\]\) + V\[N\], F\(N-1, C\)\) 



reference：http://www.importnew.com/13072.html

Decode ways

```java
public int numDecodings(String s) {
    if(s==null||s.length=0)
    return 0;
    int[] dp=new int[s.length()+1];
    dp[0]=0;
    for(int i=0;i<s.length();i++){
        if(i>1&&s.charAt(i)==0&&(s.charAt(i-1)==0||s.charAt(i-1)>2))
        return 0;

        if(s.charAt(i)!=0)
        dp[i+1]+=dp[i];
        if(s.charAt(i-1)==1||s.charAt(i-1)==2&&s.charAt(i)<=6)
        dp[i+1]=dp[i-1];
    }
    return dp[s.length()];
}
```



Reference:

https://www.topcoder.com/community/data-science/data-science-tutorials/how-to-find-a-solution/

