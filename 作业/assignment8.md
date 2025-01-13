# Assignment #8: 田忌赛马来了

Updated 1021 GMT+8 Nov 12, 2024

2024 fall, Complied by <mark>同学的姓名、院系</mark> 彭凌越 光华管理学院



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 12558: 岛屿周⻓

matices, http://cs101.openjudge.cn/practice/12558/ 

思路：每个正方形边长4，若有连接-2



代码：

```python
n,m = map(int,input().split())
lst = []
ans = 0
for i in range(n):
    lst.append(list(map(int,input().split())))
for k in range(n):
    for l in range(m):
        if lst[k][l] ==1:
            ans +=4
            if l<m-1 and lst[k][l+1]==1:
                ans-=2
            if k<n-1 and lst[k+1][l]==1:
                ans -=2
print(ans)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241119094835070](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241119094835070.png)



### LeetCode54.螺旋矩阵

matrice, https://leetcode.cn/problems/spiral-matrix/

与OJ这个题目一样的 18106: 螺旋矩阵，http://cs101.openjudge.cn/practice/18106

思路：循环更改上下左右四个边界，顺时针添加到列表中



代码：

```python
class Solution:
    def spiralOrder(self, matrix: List[List[int]]) -> List[int]:
        ans = []
        if not matrix:
            return []
        a,b,c,d=0,len(matrix[0])-1,len(matrix)-1,0
        while True:
            for i in range(d,b+1):
                ans.append(matrix[a][i])
            a+=1
            if a>c:break
            for i in range(a,c+1):
                ans.append(matrix[i][b])
            b-=1
            if b<d:break
            for i in range(b,d-1,-1):
                ans.append(matrix[c][i])
            c-=1
            if a>c:break
            for i in range(c,a-1,-1):
                ans.append(matrix[i][d])
            d+=1 
            if d>b:break
        return ans
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20241119115056254](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241119115056254.png)



### 04133:垃圾炸弹

matrices, http://cs101.openjudge.cn/practice/04133/

思路：创建一个矩阵，算出每个位置d范围内垃圾数目的和



代码：

```python
d = int(input())
n = int(input())
map_1 = [[0] * 1025 for i in range(1025)]
for _ in range(n):
    x, y, i = map(int, input().split())
    for k in range(max(0, x - d), min(1025, x + d + 1)):
        for j in range(max(0, y - d), min(1025, y + d + 1)):
            map_1[k][j] += i
max_num = max(max(l) for l in map_1)
num = sum(l.count(max_num) for l in map_1)
print(num, max_num)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241119165050580](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241119165050580.png)



### LeetCode376.摆动序列

greedy, dp, https://leetcode.cn/problems/wiggle-subsequence/

与OJ这个题目一样的，26976:摆动序列, http://cs101.openjudge.cn/routine/26976/

思路：dp,对每个数前面是增还是减分别考虑



代码：

```python
class Solution:
    def wiggleMaxLength(self, nums: List[int]) -> int:
        if len(nums)<2:
            return len(nums)
        up = [1] + [0] * (len(nums) - 1)
        down = [1] + [0] * (len(nums) - 1)
        for i in range(1, len(nums)):
            if nums[i] > nums[i - 1]:
                up[i] = max(up[i - 1], down[i - 1] + 1)
                down[i] = down[i - 1]
            elif nums[i] < nums[i - 1]:
                up[i] = up[i - 1]
                down[i] = max(up[i - 1] + 1, down[i - 1])
            else:
                up[i] = up[i - 1]
                down[i] = down[i - 1]
        return max(up[len(nums) - 1], down[len(nums) - 1])
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241119171317509](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241119171317509.png)



### CF455A: Boredom

dp, 1500, https://codeforces.com/contest/455/problem/A

思路：dp,计算每个数出现次数，求不相邻的数的最大和



代码：

```python
n = int(input())
lst=list(map(int,input().split()))
m = max(lst)
num = [0]*(m+1)
for i in lst:
    num[i]+=1
dp = [[0, 0] for i in range(m+ 1)]
for i in range(1, m + 1):
    dp[i][0] = max(dp[i - 1][0], dp[i - 1][1])
    dp[i][1] = dp[i - 1][0] + num[i] * i
print(max(dp[m][0], dp[m][1]))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241119172731578](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241119172731578.png)



### 02287: Tian Ji -- The Horse Racing

greedy, dfs http://cs101.openjudge.cn/practice/02287

思路：dp,将田忌和齐王的马速度逆序排列，田忌前i匹马和齐王前j匹马根据（i-1,j),(i-1,j-1),(i,j-1)得出



代码：

```python
from functools import lru_cache
@lru_cache(maxsize=None)
def horse():
    while True:
        n = int(input())
        if n ==0:
            break
        else:
            a = sorted(list(map(int,input().split())),reverse=True)
            b = sorted(list(map(int,input().split())),reverse=True)
            c = [[0] * (n + 1) for _ in range(n + 1)]
            for i in range(1, n + 1):
                for j in range(1, n + 1):
                    if a[i - 1] > b[j - 1]:
                        c[i][j] = max(c[i - 1][j]-1, c[i][j - 1]-1, c[i - 1][j - 1] + 1)
                    elif a[i - 1] == b[j - 1]:
                        c[i][j] = max(c[i - 1][j]-1, c[i][j - 1]-1, c[i - 1][j - 1])
                    else:
                        c[i][j] = max(c[i - 1][j]-1, c[i][j - 1]-1, c[i - 1][j - 1]-1)
            print(c[n][n] * 200)
horse()
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241119183529379](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241119183529379.png)



## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>

有几道题目自己好不容易做出来发现比题解复杂太多了，看了题解以后积累了更巧妙优雅的思路。矩阵和dp比以前做得顺手些了，在补前面的每日选做。



