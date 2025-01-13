# Assignment #B: Dec Mock Exam大雪前一天

Updated 1649 GMT+8 Dec 5, 2024

2024 fall, Complied by <mark>同学的姓名、院系 </mark> 彭凌越 光华管理学院



**说明：**

1）⽉考： AC1<mark>（请改为同学的通过数）</mark> 。考试题⽬都在“题库（包括计概、数算题目）”⾥⾯，按照数字题号能找到，可以重新提交。作业中提交⾃⼰最满意版本的代码和截图。

2）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### E22548: 机智的股民老张

http://cs101.openjudge.cn/practice/22548/

思路：遍历，找到最大差值



代码：

```python
lst = list(map(int,input().split()))
a = lst[0]
pro = 0
for i in range(1,len(lst)):
    if lst[i]-a>pro:
        pro = lst[i]-a
    if lst[i]<a:
        a = lst[i]
print(pro)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241205214859478](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241205214859478.png)



### M28701: 炸鸡排

greedy, http://cs101.openjudge.cn/practice/28701/

思路：如果max<=sum/k,时间为sum/k,否则对除去max，k-1块重复上述操作



代码：

```python
def chic(lst,k):
    if max(lst)<=sum(lst)/k:
        return f'{sum(lst)/k:.3f}'
    else:
        lst.remove(max(lst))
        return chic(lst,k-1)
n,k = map(int,input().split())
lst = list(map(int,input().split()))
print(chic(lst,k))
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20241205224712029](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241205224712029.png)



### M20744: 土豪购物

dp, http://cs101.openjudge.cn/practice/20744/

思路：dp1都不放回，dp2放回一个



代码：

```python
lst = list(map(int, input().split(',')))
dp1 = [0] * len(lst);
dp2 = [0] * len(lst)
dp1[0] = lst[0];
dp2[0] = lst[0]
for i in range(1, len(lst)):
    dp1[i] = max(dp1[i - 1] + lst[i], lst[i])
    dp2[i] = max(dp1[i - 1], dp2[i - 1] + lst[i], lst[i])
print(max(dp2))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241207203631461](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241207203631461.png)



### T25561: 2022决战双十一

brute force, dfs, http://cs101.openjudge.cn/practice/25561/

思路：dfs，暴力遍历所有商品、商店，回溯



代码：

```python
result = float("inf")
n, m = map(int, input().split())
store_prices = [input().split() for _ in range(n)]
disc = [input().split() for _ in range(m)]
lst = [0] * m

def dfs(i, price):
    global result
    if i == n:
        jian = 0
        for t in range(m):
            st = 0
            for k in disc[t]:
                a, b = map(int, k.split('-'))
                if lst[t] >= a:
                    st = max(st, b)
            jian += st
        result = min(result, price - (price // 300) * 50 - jian)
        return
    for u in store_prices[i]:
        idx, p = map(int, u.split(':'))
        lst[idx-1] += p
        dfs(i + 1, price + p)
        lst[idx-1] -= p

dfs(0, 0)
print(result)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241209105446876](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241209105446876.png)



### T20741: 两座孤岛最短距离

dfs, bfs, http://cs101.openjudge.cn/practice/20741/

思路：dijkstra,找到一个1，以之为出发点，遇到1步数不变，遇到0步数+1，直到遇到另一个岛的1（这个思路实现起来比直接bfs简单）。考试的时候没发现输入数据没有空格www



代码：

```python
import heapq
n = int(input())
ma = []
for i in range(n):
    ma.append(list(map(int,input())))
m = len(ma[0])
dir = [(-1,0),(1,0),(0,1),(0,-1)]
for i in range(n):
    for j in range(m):
        if ma[i][j]==1:
            x1,y1=i,j
            break
def dij(x1,y1):
    q,visited=[],[[False]*m for _ in range(n)]
    heapq.heappush(q,(0,x1,y1))
    while q:
        step,x,y=heapq.heappop(q)
        if visited[x][y]:
            continue
        visited[x][y] = True
        if ma[x][y]==1 and step!=0:
            return step
        for dx,dy in dir:
            if 0<=x+dx<n and 0<=y+dy<m and not visited[x+dx][y+dy]:
                heapq.heappush(q,(step+1-ma[x+dx][y+dy],x+dx,y+dy))
print(dij(x1,y1))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241209225547136](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241209225547136.png)



### T28776: 国王游戏

greedy, http://cs101.openjudge.cn/practice/28776

思路：先试试两个大臣的情况，发现左右手乘积应该升序排列



代码：

```python
n=int(input())
a,b=map(int,input().split())
numbers=[]
for i in range(n):
    ai,bi=map(int,input().split())
    numbers.append((ai,bi))
numbers.sort(key=lambda x:(x[0]*x[1]))
result=0
for i in range(n):
    result=max(result,a//numbers[i][1])
    a*=numbers[i][0]
print(result)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241209232848796](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241209232848796.png)



## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>

考察思维的题目不够灵活想不到，考实现的题目又不够熟练导致在细节上出错、或是TLE以后不愿意轻易换一种方法导致改不对。还是要多做题，提高熟练度，并且尽量提升一点思维活跃度。



