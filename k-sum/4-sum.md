* 4Sum 

Given an array S of n integers, are there elements a, b, c, and d in S such that a + b + c + d = target? Find all **unique** quadruplets in the array which gives the sum of target.

退化到3sum再退化到2sum，利用nums\[i\]==nums\[i-1\] 和while来skip重复位置，只要solution set意味着可以sort

```
Arrays.sort(nums);

//判断fix index重复
if (i > 0 && nums[i] == nums[i - 1])
continue;

//判断two pointer 重复
while (m<n&&nums[m] == nums[m - 1])
m++;
while (m<n&&nums[n] == nums[n + 1])
n--;
```



* 4sum II （hashmap）

Given four lists A, B, C, D of integer values, compute how many tuples \(i, j, k, l\) there are such that A\[i\] + B\[j\] + C\[k\] + D\[l\] is zero.

To make problem a bit easier, **all A, B, C, D have same length of N** where 0 ≤ N ≤ 500. All integers are in the range of -2^28 to 2^28 - 1 and the result is guaranteed to be at most 2^31 - 1.

分析：1. 暴力：N^4 去尝试各种可能性

            2.进化：N^3 把前三个list的可能性遍历一遍，存到hashmap中，key是sum, value是frequency，然后O\(n\)过第四个list，找target-D\[i\]在hashmap中的存在性，rt+=map.get\(target-D\[i\]\)

            3.再进化: N^2, 把前连个list 遍历一遍，存到hashmap中，key是sum, value是frequency，然后O\(n^2\)遍历后两个list，找target-C\[i\]-C\[j\]在hashmap中的存在性

```java
 public int fourSumCount(int[] A, int[] B, int[] C, int[] D) {
 Map<Integer, Integer> map = new HashMap<>();
 map.put(sum, map.getOrDefault(sum, 0) + 1);
 int res=0;
 res += map.getOrDefault(target-(A[i]+B[j]), 0);
 ｝
```



