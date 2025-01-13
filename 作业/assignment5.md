# Assignment #5: Greedy穷举Implementation

Updated 1939 GMT+8 Oct 21, 2024

2024 fall, Complied by <mark>同学的姓名、院系</mark>彭凌越，光华管理学院



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 04148: 生理周期

brute force, http://cs101.openjudge.cn/practice/04148

思路：最近一天与前三个数字的差分别为23,28,33的倍数

用时约20min



代码：

```python
k=0
while True:
    a,b,c,d=map(int,input().split())
    k+=1
    if a+b+c+d==-4:
        break

    for i in range(d+1,d+21253):
        if (i-a)%23==0 and (i-b)%28==0 and (i-c)%33==0:
            print("Case {}: the next triple peak occurs in {} days.".format(k,i-d))
            break
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241028140645371](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241028140645371.png)



### 18211: 军备竞赛

greedy, two pointers, http://cs101.openjudge.cn/practice/18211

思路：先将列表排序，然后不断制作前面的，卖出后面的；但是双指针会简单很多



代码：

```python
def make_tool(n,lst):
    ans = 0
    res = 0
    for i in range(len(lst)):
        if n - lst[0]>=0:
            ans+=1
            n-=lst[0]
            res = i
            lst = lst[1:]
        else:
            break
    return res,ans,n,lst


n = int(input())
lst = list(map(int,input().split()))
lst.sort()
if lst[0] > n:
    print(0)
else:
    res, ans,n,lst = make_tool(n, lst)
    for k in range(-1, -len(lst)-2, -1):
        try:
            if n+lst[k] >= lst[0]+lst[1]:
                n += lst[k]
                res, anss,n,lst= make_tool(n, lst)
                ans += anss-1
            else:
                if ans >0:
                    n += lst[k]
                    res, anss, n, lst = make_tool(n, lst)
                    ans += anss - 1
                else:
                    break
        except:
            break
    print(ans)
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20241028195814009](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241028195814009.png)



### 21554: 排队做实验

greedy, http://cs101.openjudge.cn/practice/21554

思路：用enumerate()排序

用时约15min

代码：

```python
n = int(input())
lst = list(map(int,input().split()))
lt = sorted(enumerate(lst,1),key=lambda x:x[1])
res = [i[0] for i in lt]
print(*res)
ans = 0
for k in range(len(lst)):
    ans += (len(lst)-k-1)*lt[k][1]
print(f'{ans/len(lst):.2f}')
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241028202620454](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241028202620454.png)



### 01008: Maya Calendar

implementation, http://cs101.openjudge.cn/practice/01008/

思路：天数不要加1，不然260整数倍时会出现问题；一直WA，看了好久才发现没有print(n)



代码：

```python
n = int(input())
print(n)
for i in range(n):
    lst = input().split()
    a = int(lst[0].strip('.'))
    c = int(lst[2])
    dic = {'pop':1, 'no':2, "zip":3, 'zotz':4, 'tzec':5, 'xul':6, 'yoxkin':7, 'mol':8, 'chen':9, 'yax':10, 'zac':11, 'ceh':12, 'mac':13, 'kankin':14, 'muan':15, 'pax':16, 'koyab':17, 'cumhu':18,'uayet':19}
    b = dic[lst[1]]
    day = 365*c + (b-1)*20 +a
    y = day //260
    d = day - y*260
    num = d %13
    n = d%20
    name=['imix', 'ik', 'akbal', 'kan', 'chicchan', 'cimi', 'manik', 'lamat', 'muluk', 'ok', 'chuen', 'eb', 'ben', 'ix', 'mem', 'cib', 'caban', 'eznab', 'canac', 'ahau']
    na = name[n]
    print(str(num+1)+' '+na+' '+str(y))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241028214736993](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241028214736993.png)



### 545C. Woodcutters

dp, greedy, 1500, https://codeforces.com/problemset/problem/545/C

思路：按顺序算每棵树，倒下后更新坐标



代码：

```python
n = int(input())
if n == 1:
    print(1)
else:
    ans = 2
    lst = []
    for i in range(n):
        lst.append(list(map(int,input().split())))
    for k in range(1,n-1):
        if lst[k][0]-lst[k-1][0]>lst[k][1]:
            ans += 1
        elif lst[k+1][0]-lst[k][0]>lst[k][1]:
            ans += 1
            lst[k][0]+=lst[k][1]
    print(ans)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241028220827552](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241028220827552.png)



### 01328: Radar Installation

greedy, http://cs101.openjudge.cn/practice/01328/

思路：从左到右计算每个岛能被覆盖的范围，有重叠就减去



代码：

```python
import math


def radar(n,d,il):
    r = []
    if d < 0:
        return -1
    for x,y in il:
        if y>d:
            return -1
        h = math.sqrt(d**2-y**2)
        r.append((x-h,x+h))
    r.sort(key=lambda x:x[1])
    ans = 1
    now = r[0][1]
    for k in range(1,n):
        if r[k][0]>now:
            ans += 1
            now = r[k][1]
    return ans
num = 0
while True:
    try:
        num+=1
        il=[]
        n,d = map(int,input().split())
        for i in range(n):
            il.append(list(map(int,input().split())))
        ans = radar(n,d,il)
        input()
        print(f'Case {num}: {ans}')
    except:
        break
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241029134403976](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241029134403976.png)



## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>

现在看到题目基本都能有思路，但有的题目因为没有想到最简单的思路导致代码非常复杂，中间出错。数学思维和算法非常重要，双指针很好用，一些题目优先用双指针做会很简洁。作业踩了一些坑，还是要仔细读题，看清楚输入输出。不小心把脚搞骨折了以后各种事情实在太多了，每日选做落下了一点，期中后一定要补上。



