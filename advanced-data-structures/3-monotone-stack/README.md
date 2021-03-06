# 3 Monotonous Stack

单调栈分的细有四种（递增或者递减），主要在于是不是严格单调，看情况和使用场景选用，比如栈里是否存在相等的元素

栈里通常存放下标或者元素，可以正向遍历或者反向遍历

**想找 "从当前元素向某一方向的第一个 (大于 / 小于) 自己的元素"，就要靠单调栈来维护单调性，对应的是 (递减 / 递增)。**

不用刻意去记（**peek大就是递增，小就是递减，有等于时是严格单调**），主要想一下什么大小关系会导致栈进行pop，比如

* What? 栈中只保存升序序列
* How? 新元素插入前 pop 掉所有比它大的
* stack(\[1,2,8,10]).push(5) => stack(\[1,2,5])

顺便提一下[Longest Increasing Subsequence](https://leetcode.com/problems/longest-increasing-subsequence/) (LIS) 问题，其实和但单调栈思路类似
