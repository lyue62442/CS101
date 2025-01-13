# Assignment #D: 十全十美 

Updated 1254 GMT+8 Dec 17, 2024

2024 fall, Complied by <mark>同学的姓名、院系</mark> 彭凌越 光华管理学院



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 02692: 假币问题

brute force, http://cs101.openjudge.cn/practice/02692

思路：一样重的一定是真的，同时处于up和down的也是真的



代码：

```python
n = int(input())
letter = ['A','B','C','D','E','F','G','H','I','J','K','L']
for i in range(n):
    good = set()
    light = set()
    heavy = set()
    #fake_pro = set()
    lst = [input().split() for _ in range(3)]
    for k in range(3):
        if lst[k][2] == 'even':
            good.update(lst[k][0])
            good.update(lst[k][1])
    for k in range(3):
        if lst[k][2] == 'up':
            light.update(lst[k][1])
            heavy.update(lst[k][0])
        elif lst[k][2]=='down':
            light.update(lst[k][0])
            heavy.update(lst[k][1])
    for u in light:
        if u in heavy:
            good.add(u)
    for t in letter:
        if t not in good:
            if t in heavy:
                print(t+' is the counterfeit coin and it is heavy.')
            else:
                print(t+' is the counterfeit coin and it is light.')
            break
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241217173133135](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241217173133135.png)



### 01088: 滑雪

dp, dfs similar, http://cs101.openjudge.cn/practice/01088

思路：如果某点的值已经算过就直接输出



代码：

```python
r, c = map(int, input().split())
ma = [list(map(int, input().split())) for _ in range(r)]
dp = [[-1]*c for _ in range(r)]
dx = [-1, 0, 1, 0]
dy = [0, 1, 0, -1]

def dfs(x, y):
    if dp[x][y] != -1:
        return dp[x][y]
    dp[x][y] = 1
    for i in range(4):
        nx, ny = x + dx[i], y + dy[i]
        if 0 <= nx < r and 0 <= ny < c and ma[x][y] > ma[nx][ny]:
            dp[x][y] = max(dp[x][y], dfs(nx, ny) + 1)
    return dp[x][y]

for x in range(r):
    for y in range(c):
        dfs(x, y)
print(max(max(row) for row in dp))
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20241218153918587](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241218153918587.png)



### 25572: 螃蟹采蘑菇

bfs, dfs, http://cs101.openjudge.cn/practice/25572/

思路：只把前面那个点入队，并通过位置关系考虑另一个点



代码：

```python
from collections import deque
n = int(input())
mat = []
for i in range(n):
    mat.append(list(map(int, input().split())))
a = []
for i in range(n):
    for j in range(n):
        if mat[i][j] == 5:
            a.append([i, j])
lx = a[1][0] - a[0][0]
ly = a[1][1] - a[0][1]
dire = [[-1, 0], [0, 1], [1, 0], [0, -1]]
v = set()


def bfs(x, y):
    v.add((x,y))
    q = deque([(x, y)])
    while q:
        x, y = q.popleft()
        if (mat[x][y] == 9 and mat[x + lx][y + ly] != 1) or mat[x][y] != 1 and mat[x + lx][y + ly] == 9:
            return 'yes'
        for i in range(4):
            dx = x + dire[i][0]
            dy = y + dire[i][1]
            if 0 <= dx < n and 0 <= dy < n and 0 <= dx + lx < n and 0 <= dy + ly < n and (dx,dy) not in v and mat[dx][dy] != 1 and mat[dx + lx][dy + ly] != 1:
                q.append((dx, dy))
                v.add((dx,dy))
    return 'no'


print(bfs(a[0][0], a[0][1]))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241218163901577](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241218163901577.png)



### 27373: 最大整数

dp, http://cs101.openjudge.cn/practice/27373/

思路：先冒泡排序再01背包，用滚动数组优化。没想到用冒泡排序



代码：

```python
def f(s):
    if s=='':
        return 0
    else:
        return int(s)
m=int(input())
n=int(input())
l=input().split()
for i in range(n):
    for j in range(n-1-i):
        if l[j] + l[j+1] > l[j+1] + l[j]:
            l[j],l[j+1] = l[j+1],l[j]
weight=[]
for num in l:
    weight.append(len(num))
dp=['']*(m+1)
for i in range(1,n+1):
    for j in range(m,0,-1):
        if weight[i-1]<=j:
            dp[j]=str(max(f(dp[j]),int(l[i-1]+dp[j-weight[i-1]])))
print(dp[m])
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241218192526027](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241218192526027.png)



### 02811: 熄灯问题

brute force, http://cs101.openjudge.cn/practice/02811

思路：有提示但还是没办法自己形成思路……深拷贝是因为list里面是可变对象，如果是int等不可变对象可以直接浅拷贝



代码：

```python
X = [[0,0,0,0,0,0,0,0]]
Y = [[0,0,0,0,0,0,0,0]]
for _ in range(5):
    X.append([0] + [int(x) for x in input().split()] + [0])
    Y.append([0 for x in range(8)])    
X.append([0,0,0,0,0,0,0,0])
Y.append([0,0,0,0,0,0,0,0])
import copy
for a in range(2):
    Y[1][1] = a
    for b in range(2):
        Y[1][2] = b
        for c in range(2):
            Y[1][3] = c
            for d in range(2):
                Y[1][4] = d
                for e in range(2):
                    Y[1][5] = e
                    for f in range(2):
                        Y[1][6] = f
                        A = copy.deepcopy(X)
                        B = copy.deepcopy(Y)
                        for i in range(1, 7):
                            if B[1][i] == 1:
                                A[1][i] = abs(A[1][i] - 1)
                                A[1][i-1] = abs(A[1][i-1] - 1)
                                A[1][i+1] = abs(A[1][i+1] - 1)
                                A[2][i] = abs(A[2][i] - 1)
                        for i in range(2, 6):
                            for j in range(1, 7):
                                if A[i-1][j] == 1:
                                    B[i][j] = 1
                                    A[i][j] = abs(A[i][j] - 1)
                                    A[i-1][j] = abs(A[i-1][j] - 1)
                                    A[i+1][j] = abs(A[i+1][j] - 1)
                                    A[i][j-1] = abs(A[i][j-1] - 1)
                                    A[i][j+1] = abs(A[i][j+1] - 1)
                        if A[5][1]==0 and A[5][2]==0 and A[5][3]==0 and A[5][4]==0 and A[5][5]==0 and A[5][6]==0:
                            for i in range(1, 6):
                                print(" ".join(repr(y) for y in [B[i][1],B[i][2],B[i][3],B[i][4],B[i][5],B[i][6]]))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241218205321938](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241218205321938.png)



### 08210: 河中跳房子

binary search, greedy, http://cs101.openjudge.cn/practice/08210/

思路：二分查找，将每个长度需移除的个数与m比较



代码：

```python
L, n, m = map(int, input().split())
rock = [0]
for i in range(n):
    rock.append(int(input()))
rock.append(L)


def throw(x):
    num = 0
    now = 0
    for i in range(1, n + 2):
        if rock[i] - now < x:
            num += 1
        else:
            now = rock[i]
    if num > m:
        return True
    else:
        return False


s,e=0,L+1
ans = -1
while s<e:
    mi=(s+e)//2
    if throw(mi):
        e=mi
    else:
        s = mi+1
        ans = mi
print(ans)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241218214753908](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241218214753908.png)



## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>

复习了讲义dp，dfs，bfs和二分查找的题目，做了一些每日选做。做题速度还是不够快，较难的greedy还是找不到思路。



