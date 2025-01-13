# Assignment #4: T-primes + 贪心

Updated 0337 GMT+8 Oct 15, 2024

2024 fall, Complied by <mark>同学的姓名、院系</mark>彭凌越，光华管理学院



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）课程网站是Canvas平台, https://pku.instructure.com, 学校通知9月19日导入选课名单后启用。**作业写好后，保留在自己手中，待9月20日提交。**

提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 34B. Sale

greedy, sorting, 900, https://codeforces.com/problemset/problem/34/B



思路：只考虑负的最多的



代码

```python
n, m = map(int, input().split())
a = list(map(int, input().split()))
a.sort()  
result = 0
for i in range(m):
    if a[i] > 0:
        break
    result += a[i]
print(-result)

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241017210012800](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241017210012800.png)



### 160A. Twins

greedy, sortings, 900, https://codeforces.com/problemset/problem/160/A

思路：优先选择较大的几个，直到大于一半



代码

```python
a = int(input())
number = list(map(int, input().split()))
number.sort(reverse=True)
s = sum(number)
c = 0
for i in range(len(number)):
    c += number[i]
    if c*2 > s:
        break
print(i + 1)

```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20241017211348894](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241017211348894.png)



### 1879B. Chips on the Board

constructive algorithms, greedy, 900, https://codeforces.com/problemset/problem/1879/B

思路： 先排序，然后一列全部选最小的数，再比大小



代码

```python
n = int(input())
for i in range(n):
    k = int(input())
    a = sorted(list(map(int, input().split())))
    b = sorted(list(map(int, input().split())))
    res = min(min(a)*k + sum(b), min(b)*k+sum(a))
    print(res)

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241018211340575](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241018211340575.png)



### 158B. Taxi

*special problem, greedy, implementation, 1100, https://codeforces.com/problemset/problem/158/B

思路：4人的一组，3人和1人一组，2人的2组一起，再看剩下的



代码

```python
import math

n = int(input())
count = 0
lst = list(map(int,input().split()))
#lst.sort(reverse=True)
count += lst.count(4)
a = lst.count(1)
b = lst.count(2)
c = lst.count(3)
count += c+math.ceil(b/2)
a -= c + b%2*2
if a <=0:
    print(count)
else:
    print(count +math.ceil(a/4))

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241020144019050](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241020144019050.png)



### *230B. T-primes（选做）

binary search, implementation, math, number theory, 1300, http://codeforces.com/problemset/problem/230/B

思路：先构建质数列表，符合条件的数是质数的平方，要用欧拉筛（这个题改了2h+才ac



代码

```python
import math

def euler(l):
    is_prime = [0 for i in range(l+1)]
    primes = []
    for i in range(2, l+1):
        if is_prime[i] == 0:
            primes.append(i)
        for p in primes:
            if i * p > l:
                break
            is_prime[i * p] = 1
            if i % p == 0:
                break
    return is_prime

is_prime = euler(1000000)

n = int(input())
nums = list(map(int, input().split()))
for num in nums:
    if num < 4:
        print('NO')
    elif int(math.sqrt(num)) ** 2 != num:
        print('NO')
    elif is_prime[int(math.sqrt(num))]:
        print('NO')
    else:
        print('YES')


```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241021112101161](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241021112101161.png)



### *12559: 最大最小整数 （选做）

greedy, strings, sortings, http://cs101.openjudge.cn/practice/12559

思路:冒泡排序，对字符串两两比较大小



代码

```python
n = int(input())
nums = input().split()
for i in range(n - 1):
    for k in range(i+1, n):
        if nums[i] + nums[k] < nums[k] + nums[i]:
            nums[i], nums[k] = nums[k], nums[i]
ans = "".join(nums)
nums.reverse()
print(ans + " " + "".join(nums))

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241021121049578](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241021121049578.png)



## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>

这周先是熬夜备赛，后来又踩空崴了脚，加上各种ddl，感觉生活好像要乱成一锅粥了www。但还是在努力跟上每日选做，落下的一小部分争取下周赶上。

感觉最近的题目挺难的，自己做总是很久还是WA或者超时，但看了题解以后豁然开朗，积累了一些不错的方法。希望以后能做得更顺手些。

