https://atcoder.jp/contests/agc065/tasks/agc065_a  
https://atcoder.jp/contests/agc065/editorial/8011  


重排输入序列，使相邻差值取mod后求和最大化  

首先可以发现其中的不变量，差值的总和是不变的，我们只需要把这些差值安排好对应的位置。显然让差值每次取-1是最好的，因为(-1 mod k)就是(k-1)，显然是最大值，差一点的当然是-2，-3这样。这样的贪心策略其实就是在mod k的环上一次次拿前一个东西。  
考虑其中的不变量会发现，如果我们把序列尾项和首项的差值也算上，那最终答案的最大值就是这样一直转圈的结果，现在少了这一项，就要再找一下这样转圈的过程中跳的最远的一次，也就是对应了-(k-eps)。  

随便一个数据结构能找上一项就行。

## tags：

- mod加性最优化
- 不变量
- arg max/min
- 值域相关

给定了一个长度为 $N$ 的序列 $A=\{A_1,A_2,A_3,...,A_N\}$ ，还给定了一个模数 $K$ 。  
现在你可以把这个序列以任意方式重新排列，使得重排后的序列 $A^\prime$ 的如下指标最大化，并输出这一指标的数值：
```math
\sum^{N-1}_{i=1}((A^{\prime}_{i+1}-A^{\prime}_i)\mod K)
```

```
Contest Duration: 2023-12-17(Sun) 20:00 - 2023-12-17(Sun) 23:00 (local time) (180 minutes)Back to Home
 Top
 Tasks
 Clarifications
 Results
 Standings
 Virtual Standings
 Editorial
 Discuss
A - Shuffle and mod K  / 
Time Limit: 2 sec / Memory Limit: 1024 MB

Score : 
500 points

Problem Statement
You are given an integer sequence 
A=(A 
1
​
 ,A 
2
​
 ,…,A 
N
​
 ) of length 
N.

You can rearrange 
A freely. Find the maximum value that 
∑ 
i=1
N−1
​
 ((A 
i+1
​
 −A 
i
​
 )modK) can take after rearranging.

Here, 
xmodK denotes the integer 
y such that 
0≤y<K and 
x−y is a multiple of 
K. For example, 
−3mod8=5, and 
9mod6=3.

Constraints
2≤N≤2×10 
5
 
1≤K≤10 
9
 
0≤A 
i
​
 <K
Input
The input is given from Standard Input in the following format:

N 
K
A 
1
​
  
A 
2
​
  
… 
A 
N
​
 
Output
Print the answer.

Sample Input 1
Copy
3 4
0 1 2
Sample Output 1
Copy
6
One optimal solution is to rearrange 
A into 
(2,1,0) to achieve 
(1−2)mod4+(0−1)mod4=3+3=6.

Sample Input 2
Copy
7 123
11 34 56 0 32 100 78
Sample Output 2
Copy
638
```
