# Assignment #A: dp & bfs

Updated 2 GMT+8 Nov 25, 2024

2024 fall, Complied by <mark>同学的姓名、院系</mark> 彭凌越 光华管理学院



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### LuoguP1255 数楼梯

dp, bfs, https://www.luogu.com.cn/problem/P1255

思路：dp，等于前两级的方法数之和



代码：

```python
n = int(input())
dp = [0] * (n + 1)
dp[0] = 1
for i in range(1, n+1):
    if i >= 2:
        dp[i] = dp[i-1] + dp[i-2]
    else:
        dp[i] = 1
print(dp[n])
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241203134326093](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241203134326093.png)



### 27528: 跳台阶

dp, http://cs101.openjudge.cn/practice/27528/

思路：dp，等于前面所有台阶的方法数之和



代码：

```python
n = int(input())
dp = [0]*(n+1)
dp[0]=1
for i in range(n+1):
    for k in range(i):
        dp[i]+=dp[k]
print(dp[n])
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20241203135445245](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241203135445245.png)



### 474D. Flowers

dp, https://codeforces.com/problemset/problem/474/D

思路：dp，和跳台阶相同，用前缀和防止超时



代码：

```python
mod = 1000000007
t, k = map(int, input().split())
dp = [0] * 100001
dp[0] = 1
s = [0] * 100001
for i in range(1, 100001):
    if i >= k:
        dp[i] = (dp[i-1] + dp[i - k]) % mod
    else:
        dp[i] = dp[i - 1]
    s[i] = (s[i - 1] + dp[i]) % mod
for _ in range(t):
    a, b = map(int, input().split())
    print((s[b] - s[a - 1] + mod) % mod)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241203150034950](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241203150034950.png)



### LeetCode5.最长回文子串

dp, two pointers, string, https://leetcode.cn/problems/longest-palindromic-substring/

思路：dp，回文串需要去掉首尾还是回文



代码：

```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        n = len(s)
        if n < 2:
            return s
        max_len = 1
        fr = 0
        dp = [[False] * n for _ in range(n)]
        for i in range(n):
            dp[i][i] = True
        for l in range(2, n + 1):
            for i in range(n):
                j = l + i - 1
                if j >= n:
                    break
                if s[i] != s[j]:
                    dp[i][j] = False
                else:
                    if j - i < 3:
                        dp[i][j] = True
                    else:
                        dp[i][j] = dp[i + 1][j - 1]
                if dp[i][j] and j - i + 1 > max_len:
                    max_len = j - i + 1
                    fr = i
        return s[fr:fr + max_len]
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241203152312544](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241203152312544.png)





### 12029: 水淹七军

bfs, dfs, http://cs101.openjudge.cn/practice/12029/

思路：dfs，一直RE, 后来才发现要用input = sys.stdin.read一次性读入



代码：

```python
import sys
sys.setrecursionlimit(300000)
input = sys.stdin.read

def is_valid(x, y, m, n):
    return 0 <= x < m and 0 <= y < n

def dfs(x, y, height, m, n, ma, water):
    dx = [-1, 1, 0, 0]
    dy = [0, 0, -1, 1]
    for i in range(4):
        nx, ny = x + dx[i], y + dy[i]
        if is_valid(nx, ny, m, n) and ma[nx][ny] < height:
            if water[nx][ny] < height:
                water[x][y] = height
                dfs(nx, ny, height, m, n, ma, water)

def main():
    data = input().split()
    idx = 0
    k = int(data[idx])
    idx += 1
    results = []
    for _ in range(k):
        m, n = map(int, data[idx:idx + 2])
        idx += 2
        ma = []
        for i in range(m):
            ma.append(list(map(int, data[idx:idx + n])))
            idx += n
        water = [[0] * n for _ in range(m)]
        i, j = map(int, data[idx:idx + 2])
        idx += 2
        i, j = i - 1, j - 1
        p = int(data[idx])
        idx += 1
        for _ in range(p):
            x, y = map(int, data[idx:idx + 2])
            idx += 2
            x, y = x - 1, y - 1
            if ma[x][y] <= ma[i][j]:
                continue
        dfs(x, y, ma[x][y], m, n, ma, water)
        results.append("Yes" if water[i][j] > 0 else "No")
    sys.stdout.write("\n".join(results) + "\n")

if __name__ == "__main__":
    main()
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241203164714401](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241203164714401.png)



### 02802: 小游戏

bfs, http://cs101.openjudge.cn/practice/02802/

思路：bfs，在外面加保护圈，如果方向改变线段加一



代码：

```python
from collections import deque

def bfs(s, e, board, h, w):
    queue = deque([s])
    in_queue = set()
    dir = [(0, -1), (-1, 0), (0, 1), (1, 0)]
    ans = []
    while queue:
        x, y, dirs, seg = queue.popleft()
        if (x, y) == e:
            ans.append(seg)
            break
        for i, (dx, dy) in enumerate(dir):
            nx, ny = x + dx, y + dy
            if 0 <= nx < h + 2 and 0 <= ny < w + 2 and ((nx, ny, i) not in in_queue):
                new_dir = i
                new_seg = seg if new_dir == dirs else seg + 1
                if (nx, ny) == e:
                    ans.append(new_seg)
                    continue
                if board[nx][ny] != 'X':
                    in_queue.add((nx, ny, i))
                    queue.append((nx, ny, new_dir, new_seg))
    if len(ans) == 0:
        return -1
    else:
        return min(ans)
board_num = 1
while True:
    w, h = map(int, input().split())
    if w == h == 0: break
    board = [' ' * (w + 2)] + [' ' + input() + ' ' for _ in range(h)] + [' ' * (w + 2)]
    print(f"Board #{board_num}:")
    pair_num = 1
    while True:
        y1, x1, y2, x2 = map(int, input().split())
        if x1 == y1 == x2 == y2 == 0: 
            break
        s = (x1, y1, -1, 0)
        e = (x2, y2)
        seg = bfs(s, e, board, h, w)
        if seg == -1: 
            print(f"Pair {pair_num}: impossible.")
        else: 
            print(f"Pair {pair_num}: {seg} segments.")
        pair_num += 1
    print()
    board_num += 1
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241203171451369](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241203171451369.png)



## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>

题目思路基本都没什么问题，大部分可以套模版，但是长的题目熟练度不够总是出错，还是要多做题。学会了用input = sys.stdin.read一次性读入数据。在努力赶上每日选做。





