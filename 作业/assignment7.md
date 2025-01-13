# Assignment #7: Nov Mock Exam立冬

Updated 1646 GMT+8 Nov 7, 2024

2024 fall, Complied by <mark>同学的姓名、院系</mark> 彭凌越 光华管理学院



**说明：**

1）⽉考： AC5<mark>（请改为同学的通过数）</mark> 。考试题⽬都在“题库（包括计概、数算题目）”⾥⾯，按照数字题号能找到，可以重新提交。作业中提交⾃⼰最满意版本的代码和截图。

2）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### E07618: 病人排队

sorttings, http://cs101.openjudge.cn/practice/07618/

思路：对60岁以上和60岁以下用两个列表分别排列

用时约13min



代码：

```python
n = int(input())
lst = []
young = []
for i in range(n):
    a,b = map(str,input().split())
    b = int(b)
    if b>=60:
        lst.append([a,b])
    else:
        young.append([a,b])
lst.sort(key=lambda x:x[1],reverse=True)
for k in range(len(lst)):
    print(str(lst[k][0]))
for m in range(len(young)):
    print(str(young[m][0]))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241112154223485](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241112154223485.png)



### E23555: 节省存储的矩阵乘法

implementation, matrices, http://cs101.openjudge.cn/practice/23555/

思路：直接写成矩阵再相乘

用时约15min

代码：

```python
n,m1,m2=map(int,input().split())
a = [[0]*n for i in range(n)]
b = [[0]*n for l in range(n)]
c = [[0]*n for m in range(n)]
for i in range(m1):
    x,y,k=map(int,input().split())
    a[x][y]=k
for i in range(m2):
    x,y,k=map(int,input().split())
    b[x][y]=k
for i in range(n):
    for j in range(n):
        c[i][j]=sum(a[i][t]*b[t][j] for t in range(n))
        if c[i][j]!=0:
            print(i,j,c[i][j])
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20241112161144757](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241112161144757.png)



### M18182: 打怪兽 

implementation/sortings/data structures, http://cs101.openjudge.cn/practice/18182/

思路：对ti升序，xi降序排序循环，但中间不小心把索引1写成0，检查了好久才发现

用时约35min

代码：

```python
case = int(input())
for i in range(case):
    found = False
    lst = []
    n,m,b=map(int,input().split())
    for k in range(n):
        t,x = map(int,input().split())
        lst.append([t,x])
    lst.sort(key=lambda x:(x[0],-x[1]))
    m1 = m-1
    b-=lst[0][1]
    if b<=0:
        print(lst[0][0])
        found = True
    else:
        for u in range(1,len(lst)):
            if lst[u][0]==lst[u-1][0]:
                if m1>=1:
                    m1 -= 1
                    b-=lst[u][1]
            else:
                m1 = m-1
                b-=lst[u][1]
            if b<=0:
                print(lst[u][0])
                found = True
                break
    if not found:
        print("alive")
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241112165913444](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241112165913444.png)



### M28780: 零钱兑换3

dp, http://cs101.openjudge.cn/practice/28780/

思路：dp,每种金额的数目为min(inf,该金额-硬币金额数目+1)，上次作业有类似的题，但还是不太熟，还是推了一会儿

用时约30min

代码：

```python
from math import inf
n,m =map(int,input().split())
lst = list(map(int,input().split()))
lst.sort(reverse=True)
dp = [0] + [inf for i in range(m)]
for i in range(n):
    for j in range(lst[i], m + 1):
        dp[j] = min(dp[j], dp[j - lst[i]] + 1)
print(dp[m] if dp[m] != inf else -1)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241112171745701](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241112171745701.png)



### T12757: 阿尔法星人翻译官

implementation, http://cs101.openjudge.cn/practice/12757

思路：储存hundred,遍历到thousand,million再结算。但自己做的时候没想到这样做就没做出来，看题解后觉得很巧妙

用时45min+

代码：

```python
n = list(map(str,input().split()))
dic = {"zero": 0, "one": 1, "two": 2, "three": 3, "four": 4, "five": 5, "six": 6,
       "seven": 7, "eight": 8, "nine": 9, "ten": 10, "eleven": 11, "twelve": 12,
       "thirteen": 13, "fourteen": 14, "fifteen": 15, "sixteen": 16, "seventeen": 17,
       "eighteen": 18, "nineteen": 19, "twenty": 20, "thirty": 30, "forty": 40,
       "fifty": 50, "sixty": 60, "seventy": 70, "eighty": 80, "ninety": 90,
       "hundred": 100, "thousand": 1000, "million": 1000000}
first = 1
if n[0] == "negative":
    first = -1
    del n[0]
total = 0
t = 0
for i in n:
    if i in ("thousand", "million"):
        total += t * dic[i]
        t = 0
        continue
    if i == "hundred":
        t *= dic[i]
    else:
        t += dic[i]
print(first * (total + t))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241112200401023](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241112200401023.png)



### T16528: 充实的寒假生活

greedy/dp, cs10117 Final Exam, http://cs101.openjudge.cn/practice/16528/

思路：greedy，按结束时间顺序排序

用时约15min

代码：

```python
n = int(input())
lst = []
ans = 1
for i in range(n):
    lst.append(list(map(int,input().split())))
lst.sort(key=lambda x:x[1])
time = lst[0][1]
for k in range(1,n):
    if lst[k][0]>60:
        break
    else:
        if lst[k][0]>time and lst[k][1]<=60:
            ans +=1
            time = lst[k][1]
print(ans)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241112185353579](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241112185353579.png)



## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>

没有参加月考，所以是自己限时做的。第五题感觉好麻烦就直接跳过了，做完其他题目才回头来看，还是缺少一点看出题目本质的思维。期中考试终于结束了，从这周开始要把前面的每日选做补起来，多做一点递归和dp。



