# Assignment #9: dfs, bfs, & dp

Updated 2107 GMT+8 Nov 19, 2024

2024 fall, Complied by <mark>同学的姓名、院系</mark> 彭凌越 光华管理学院



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 18160: 最大连通域面积

dfs similar, http://cs101.openjudge.cn/practice/18160

思路：dfs,遍历矩阵，计算每个连通水域的面积，记录最大值



代码：

```python
dir = [[-1,-1],[-1,0],[-1,1],[0,-1],[0,1],[1,-1],[1,0],[1,1]]

def dfs(x, y, matrix, area=0):
    if matrix[x][y] == '.':
        return area
    matrix[x][y] = '.'
    area += 1
    for dx, dy in dir:
        area = dfs(x + dx, y + dy, matrix, area)
    return area

for _ in range(int(input())):
    n, m = map(int, input().split())
    matrix = [['.' for _ in range(m + 2)] for _ in range(n + 2)]
    for i in range(1, n + 1):
        matrix[i][1:-1] = list(input())
    res = 0
    for i in range(1, n + 1):
        for j in range(1, m + 1):
            if matrix[i][j] == 'W':
                area = dfs(i, j, matrix)
                res = max(res, area)
    print(res)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241126170856450](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241126170856450.png)



### 19930: 寻宝

bfs, http://cs101.openjudge.cn/practice/19930

思路：bfs,遇到1返回步数，否则直至队列为空



代码：

```python
import heapq


def bfs(x, y):
    d = [[-1, 0], [1, 0], [0, 1], [0, -1]]
    que = []
    heapq.heappush(que, [0, x, y])
    check = set()
    check.add((x, y))
    while que:
        step, x, y = map(int, heapq.heappop(que))
        if ma[x][y] == 1:
            return step
        for i in range(4):
            dx, dy = x + d[i][0], y + d[i][1]
            if ma[dx][dy] != 2 and (dx, dy) not in check:
                heapq.heappush(que, [step + 1, dx, dy])
                check.add((dx, dy))
    return "NO"


m, n = map(int, input().split())
ma = [[2] * (n + 2)] + [[2] + list(map(int, input().split())) + [2] for i in range(m)] + [[2] * (n + 2)]
print(bfs(1, 1))
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20241126172059378](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241126172059378.png)



### 04123: 马走日

dfs, http://cs101.openjudge.cn/practice/04123

思路：dfs,遍历，将走过的标记，直至没有下一步



代码：

```python
T=int(input())
x1 = [-2, -1, 1, 2, 2, 1, -1, -2]
y1 = [1, 2, 2, 1, -1, -2, -2, -1]


def dfs(step, x, y, ans, chess):
    if n * m == step:
        return ans + 1
    for r in range(8):
        s = x + x1[r]
        t = y + y1[r]
        if 0 <= s < n and 0 <= t < m and not chess[s][t]:
            chess[s][t] = True
            ans = dfs(step + 1, s, t, ans, chess)
            chess[s][t] = False
    return ans


for _ in range(T):
    n, m, x, y = map(int, input().split())
    chess = [[False] * T for _ in range(T)]
    chess[x][y] = True
    result = dfs(1, x, y, 0, chess)
    print(result)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241126173210336](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241126173210336.png)



### sy316: 矩阵最大权值路径

dfs, https://sunnywhy.com/sfbj/8/1/316

思路：dfs,遍历，（max_path = cur_path[:]是浅复制，这样即使原始列表发生了变化，副本仍然保持不变）



代码：

```python
n, m = map(int, input().split())
maze = [list(map(int, input().split())) for _ in range(n)]
dir = [(0, 1), (1, 0), (0, -1), (-1, 0)]
visited = [[False] * m for _ in range(n)]
max_path = []
max_sum = -float('inf')

def dfs(x, y, cur_path, cur_sum):
    global max_path, max_sum
    if (x, y) == (n - 1, m - 1):
        if cur_sum > max_sum:
            max_sum = cur_sum
            <mark>max_path = cur_path[:]</mark>
        return
    for dx, dy in dir:
        nx, ny = x + dx, y + dy
        if 0 <= nx < n and 0 <= ny < m and not visited[nx][ny]:
            visited[nx][ny] = True
            cur_path.append((nx, ny))
            dfs(nx, ny, cur_path, cur_sum + maze[nx][ny])
            cur_path.pop()
            visited[nx][ny] = False

visited[0][0] = True
dfs(0, 0, [(0, 0)], maze[0][0])
for x, y in max_path:
    print(x + 1, y + 1)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241126174337543](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241126174337543.png)





### LeetCode62.不同路径

dp, https://leetcode.cn/problems/unique-paths/

思路：排列组合



代码：

```python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        ans = 1
        for i in range(m,m+n-1):
            ans *=i
        for k in range(1,n):
            ans //= k
        return ans 
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241126185814564](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241126185814564.png)



### sy358: 受到祝福的平方

dfs, dp, https://sunnywhy.com/sfbj/8/3/539

思路：dfs，从前往后看是否是平方数



代码：

```python
n = int(input())
squares = []
i = 1
while i **2 <= 10 ** 9:
    squares.append(i **2)
    i += 1
n = list(map(int, str(n)))

def dfs(l):
    if l == len(n):
        return True
    num = 0
    for i in range(l, len(n)):
        num = num * 10 + n[i]
        if num in squares:
            if dfs(i + 1):
                return True
    return False
if dfs(0):
    print('Yes')
else:
    print('No')
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241126192826638](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241126192826638.png)



## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>

基本是模版题，但因为不够熟练，所以还是做了较长时间，做完以后对dfs，bfs的题目手感提升了一些。

在补前面的每日选做，部分复杂的贪心还是不能独立做对。



