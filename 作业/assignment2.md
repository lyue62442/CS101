# Assignment #2: 语法练习

Updated 0126 GMT+8 Sep 24, 2024

2024 fall, Complied by ==同学的姓名、院系==彭凌越，光华管理学院



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）课程网站是Canvas平台, https://pku.instructure.com, 学校通知9月19日导入选课名单后启用。**作业写好后，保留在自己手中，待9月20日提交。**

提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 263A. Beautiful Matrix

https://codeforces.com/problemset/problem/263/A



思路：用标志变量found = True确定什么时候break



##### 代码

```python
lst = []
a = -1
found = False  
for i in range(5):
    lst.append(list(input().split()))
for i in range(5):
    for j in range(5):
        if lst[i][j] == "1":  
            a = abs(i - 2) + abs(j - 2)
            found = True  
            break  
    if found:  
        break
print(a)

```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240924162802691](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20240924162802691.png)



### 1328A. Divisibility Problem

https://codeforces.com/problemset/problem/1328/A



思路：次数为（第二个数减第一个数对第二个数的余数）对第一个数的余数



##### 代码

```python
n = int(input())
for i in range(n):
    lst = list(input().split())
    print((int(lst[1])-int(lst[0])%int(lst[1]))%int(lst[1]))

```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240924163129144](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20240924163129144.png)



### 427A. Police Recruits

https://codeforces.com/problemset/problem/427/A



思路：对每个出现的1和-1讨论



##### 代码

```python
a = int(input())
lst = list(map(int,input().split()))
res = 0
ans = 0
for i in range(a):
    if lst[i] > 0:
        res += lst[i]
    else:
        res += lst[i]
        if res < 0:
            ans += 1
            res = 0
print(ans)

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240925091053630](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20240925091053630.png)



### 02808: 校门外的树

http://cs101.openjudge.cn/practice/02808/



思路：

```
第一次做的时候没考虑区域重叠
学到了一种列表处理的方法，答案的写法好简洁
```



##### 代码

```python
L, M = map(int, input().split())
lst = [1]*(L+1)
for i in range(M):
    a, b = map(int, input().split())
    for n in range(a, b+1):
        lst[n] = 0
print(lst.count(1))

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240924161942984](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20240924161942984.png)



### sy60: 水仙花数II

https://sunnywhy.com/sfbj/3/1/60



思路：注意join对象是str



##### 代码

```python
lst = list(map(int, input().split()))
found = False
ans = []
for a in range(lst[0], lst[1] + 1):
    b = a // 100
    c = (a - b*100)//10
    d = a - b*100 - c*10
    if a == b**3 +c**3 + d**3:
        ans.append(str(a))
        found = True
if not found:
    print("NO")
else:
    print(" ".join(ans))

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240925101231269](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20240925101231269.png)



### 01922: Ride to School

http://cs101.openjudge.cn/practice/01922/



思路：跳过负的时间，取所有时间中的最小值



##### 代码

```python
import math
while True:
    n = int(input())
    ans = []
    if n == 0:
        break
    for i in range(n):
        lst = list(map(int, input().split()))
        if lst[1]<0:
            continue
        else:
            ti = math.ceil(lst[1]+4500/lst[0]*3.6)
            ans.append(ti)
    print(min(ans))

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240926085132370](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20240926085132370.png)



## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。==

1.做题的时候巩固了一些语法，注意到了一些以前忽略的问题，如join的对象是str不是Int等；

2.通过跟答案对比扩展了思路，如从oj2808的答案学到了一种数列处理方法，并发现可以在其他题目运用；

3.用gpt优化代码，积累了一些新的思路，如OJ3248最大公约数gpt用了辗转相除法，就比常规方法运行速度快很多；

4.在跟进每日选做，争取在国庆期间把前面的每日选做做完。



