## 题目列表 {#题目列表}

* [**2 sum II - input array is sorted**](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)
* [**2 sum III - data structure design**](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)
* [3 sum](https://leetcode.com/problems/3sum/)
* [3 sum closest](https://leetcode.com/problems/3sum-closest/)
* [**3 sum smaller**](https://leetcode.com/problems/3sum-smaller/)
* [4 sum](https://leetcode.com/problems/4sum/)
* [4 sum II](https://leetcode.com/problems/4sum-ii/#/description)
* [k sum](http://www.lintcode.com/problem/k-sum)
* [k sum II](http://www.lintcode.com/problem/k-sum)



### 方法1 - brute force {#方法1--brute-force}

枚举所有的k-subset, time complexity就是从N中选出k个,`O(n^k)`

### 方法2 - 先sort,再two pointer {#方法2--先sort再two-pointer}

O\(NlogN + N\) = O\(nlogn\), 要注意的是sort了之后就改变了原来的顺序

### 方法3 - hashmap O\(n\) {#方法3--hashmap-on}

对于2 sum来说，其实就是对于每一个element`nums[i]`, 在数组中找是否存在`target - nums[i]`

用hashmap保存访问过的value, 对每个`num[i]`,检查hashmap中是否有`target - nums[i]`,扫完一遍就能够得到结果。属于用空间换时间。

time complexity -`O(n)`space complexity -`O(n)`



对于two sum的题目

* 如果是要返回index,那么优先用hashmap的做，因为不会改变原来array的顺序
* 如果是返回元素的value,那么可以用先sort然后two pointer的方法

对于3sum, 3sum closest, 4sum等题目，因为大部分都是根据two sum two pointer做法的延伸，所以都是要求return value



