# Assignment #6: Recursion and DP

Updated 2201 GMT+8 Oct 29, 2024

2024 fall, Complied by <mark>同学的姓名、院系</mark> 彭凌越 光华管理学院



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### sy119: 汉诺塔

recursion, https://sunnywhy.com/sfbj/4/3/119  

思路：递归，base case为n=0



代码：

```python
n = int(input())
#@lru_cache(maxsize=None)
def hanno(n,fr,to,md):
    if n ==0:
        return
    hanno(n-1,fr,md,to)
    print(f'{fr}->{to}')
    hanno(n-1,md,to,fr)


print(2**n-1)
hanno(n,'A','C','B')
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241031115753115](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241031115753115.png)



### sy132: 全排列I

recursion, https://sunnywhy.com/sfbj/4/3/132

思路：用一个列表记录每个数字是否被使用，输出一组时再从后往前逐一标记为未使用，不断递归。

自己做的时候完全没思路，想不清楚怎么递归，看答案后在草稿纸上推了一遍才弄懂。

代码：

```python
n = int(input())
lst = [False]*(n+1)
def quanpai(n,pre=[]):
    if len(pre)==n:
        return [pre]
    res = []
    for i in range(1,n+1):
        if lst[i]:
            continue
        lst[i] = True
        res += quanpai(n, pre+[i])
        lst[i]=False
    return res
res = quanpai(n)
for r in res:
    print(' '.join(map(str,r)))
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20241101122840544](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241101122840544.png)



### 02945: 拦截导弹 

dp, http://cs101.openjudge.cn/2024fallroutine/02945

思路：动态规划，计算每个高度前符合的个数



代码：

```python
n = int(input())
def missile(n,lst):
    dp = [1]*n
    for i in range(1,n):
        for j in range(i):
            if lst[i]<=lst[j]:
                dp[i]=max(dp[i],dp[j]+1)
    return max(dp)


lst = list(map(int,input().split()))
print(missile(n,lst))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241102163407907](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241102163407907.png)



### 23421: 小偷背包 

dp, http://cs101.openjudge.cn/practice/23421

思路：dp,取max（不要第i个背包不变，要第i个背包减少）。math.inf：无穷大



代码：

```python
import math
n,b=map(int,input().split())
a=list(map(int,input().split()))
c = list(map(int,input().split()))


def pack(i,s):
    if s<0:
        return -math.inf
    if i == len(a):
        return 0
    return max(pack(i+1,s),a[i]+pack(i+1,s-c[i]))


print(pack(0,b))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241103092959212](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241103092959212.png)



### 02754: 八皇后

dfs and similar, http://cs101.openjudge.cn/practice/02754

思路：从第一行开始，判断后面每一行是否满足，不满足则右移（都不满足时会自动回溯到上一层）



代码：

```python
lst = []
def queen(s):
    if len(s)==8:
        lst.append(s)
        return
    for i in range(1,9):
        if all(str(i)!=s[k] and abs(len(s)-k)!=abs(i-int(s[k])) for k in range(len(s))):
            queen(s+str(i))


queen('')
n = int(input())
for i in range(n):
    b = int(input())
    print(lst[b-1])
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241103220019043](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241103220019043.png)



### 189A. Cut Ribbon 

brute force, dp 1300 https://codeforces.com/problemset/problem/189/A

思路：暴力枚举超时了，dp,与背包问题类似，从n=1时开始遍历



代码：

```python
n, a, b, c = map(int, input().split())
dp = [0]+[float('-inf')]*n
for i in range(1, n+1):
    for k in (a, b, c):
        if i >=k:
            dp[i] = max(dp[i-k] + 1, dp[i])
print(dp[n])
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241104084029136](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241104084029136.png)



## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>

这次的题目好难，大部分题自己做都没什么思路，不知道怎么递归，或是有思路但不知道怎么用代码实现。但是理解了题解以后有种豁然开朗的感觉，对递归和dp有了一定的理解。



