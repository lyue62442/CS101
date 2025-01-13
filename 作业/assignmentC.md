# Assignment #C: 五味杂陈 

Updated 1148 GMT+8 Dec 10, 2024

2024 fall, Complied by <mark>同学的姓名、院系</mark> 彭凌越 光华管理学院



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 1115. 取石子游戏

dfs, https://www.acwing.com/problem/content/description/1117/

思路：遍历先手取完后所有可能的结果，如果后手有必赢策略则lose，反之win



代码：

```python
dic = {}
def dfs(a,b):
    if (a,b) in dic:
        return dic[(a,b)]
    if a==0 or b==0:
        dic[(a,b)]=True
        return True
    if a<b:
        a,b = b,a
    if a%b==0:
        dic[(a,b)]=True
        return True
    for i in range(1,a//b+1):
            if not dfs(a-i*b,b):
                dic[(a,b)]=True
                return True
    dic[(a,b)]=False
    return False
while True:
    a, b = map(int, input().split())
    if a == 0 and b == 0:
        break
    if dfs(a,b):
        print('win')
    else:
        print('lose')
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241210221404799](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241210221404799.png)



### 25570: 洋葱

Matrices, http://cs101.openjudge.cn/practice/25570

思路：分奇偶数计算每一圈的和



代码：

```python
n = int(input())
ma=[]
ans =[]
for i in range(n):
    ma.append(list(map(int,input().split())))
for k in range(n//2):
    res = sum(ma[k][k:n-k])+sum(ma[n-k-1][k:n-k])
    for u in range(k+1,n-k-1):
        res+=ma[u][k]+ma[u][n-k-1]
    ans.append(res)
if n%2==1:
    ans.append(ma[n//2][n//2])
print(max(ans))
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20241210231240157](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241210231240157.png)



### 1526C1. Potions(Easy Version)

greedy, dp, data structures, brute force, *1500, https://codeforces.com/problemset/problem/1526/C1

思路：贪心，顺着遍历，找到每刻数量最多且和最大的情况



代码：

```python
n = int(input())
lst = list(map(int,input().split()))
res = []
ans = 0
dp = [0]*n
for i in lst:
    if ans+i>=0:
        res.append(i)
        ans+=i
    else:
        if res and i>min(res):
            ans+=i-min(res)
            res.remove(min(res))
            res.append(i)
print(len(res))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241212162030531](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241212162030531.png)



### 22067: 快速堆猪

辅助栈，http://cs101.openjudge.cn/practice/22067/

思路：辅助栈，一个栈单独存储min



代码：

```python
lst = []
m = []
while True:
    try:
        s = input().split()
        if s[0] == "pop":
            if lst:
                lst.pop()
                if m:
                    m.pop()
        elif s[0] == "min":
            if m:
                print(m[-1])
        else:
            t = int(s[1])
            lst.append(t)
            if not m:
                m.append(t)
            else:
                k = m[-1]
                m.append(min(k, t))
    except:
        break
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241212163719863](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241212163719863.png)



### 20106: 走山路

Dijkstra, http://cs101.openjudge.cn/practice/20106/

思路：heappop的时候，才能入inq，这样才能保证最短的优先访问，否则最短路径可能加不进inq



代码：

```python
import heapq
m,n,p = map(int,input().split())
ma = []
dir = [(0,1),(0,-1),(1,0),(-1,0)]
for _ in range(m):
    ma.append(input().split())
for i in range(p):
    try:
        a,b,c,d = map(int,input().split())
        queue = []
        flag = False
        inq = set()
        heapq.heappush(queue,(0,a,b))
        inq.add((a,b))
        while queue:
            step,x,y=heapq.heappop(queue)
            inq.add((x,y))
            if x==c and y==d:
                flag=True
                break
            for (dx,dy) in dir:
                nx,ny = x+dx,y+dy
                if 0<=nx<m and 0<=ny<n and ma[nx][ny]!='#' and (nx,ny) not in inq:
                    
                    heapq.heappush(queue,(step+abs(int(ma[nx][ny])-int(ma[x][y])),nx,ny))
        if flag:
            print(step)
        else:
            print('NO')
    except:
        print('NO')
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241212202122756](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241212202122756.png)



### 04129: 变换的迷宫

bfs, http://cs101.openjudge.cn/practice/04129/

思路：用 visited记录每次到达时的时间，取模，如果在K的整数倍之前到过这里，情况就与之前重复

没想到是取模操作

代码：

```python
from collections import deque

def bfs(x, y):
    visited = {(0, x, y)}
    dx = [0, 0, 1, -1]
    dy = [1, -1, 0, 0]
    queue = deque([(0, x, y)])
    while queue:
        time, x, y = queue.popleft()
        for i in range(4):
            nx, ny = x + dx[i], y + dy[i]
            te = (time + 1) % k
            if 0 <= nx < r and 0 <= ny < c and (te, nx, ny) not in visited:
                now = ma[nx][ny]
                if now == 'E':
                    return time + 1
                elif now != '#' or te == 0:
                    queue.append((time + 1, nx, ny))
                    visited.add((te, nx, ny))
    return 'Oop!'


t = int(input())
for _ in range(t):
    r, c, k = map(int, input().split())
    ma = [list(input()) for _ in range(r)]
    for i in range(r):
        for j in range(c):
            if ma[i][j] == 'S':
                print(bfs(i, j))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241214120141640](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241214120141640.png)



## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>

学会了辅助栈和dijkstra,对bfs和dfs的变型熟练一点了

在做之前的每日选做，争取至少AC5www



