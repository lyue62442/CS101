# Assignment #1: 自主学习

Updated 0110 GMT+8 Sep 10, 2024

2024 fall, Complied by ==同学的姓名、院系==彭凌越，光华管理学院



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）课程网站是Canvas平台, https://pku.instructure.com, 学校通知9月19日导入选课名单后启用。**作业写好后，保留在自己手中，待9月20日提交。**

提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 02733: 判断闰年

http://cs101.openjudge.cn/practice/02733/



思路：看除以4、3200、100、400的余数



##### 代码

```python
a = int(input())
if a % 4 == 0 and a % 3200 != 0 and a %100 != 0 or a % 400 == 0:
    print("Y")
else:
    print("N") 

```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240922165224891](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20240922165224891.png)



### 02750: 鸡兔同笼

http://cs101.openjudge.cn/practice/02750/



思路：看是否整除2、4



##### 代码

```python
a = int(input())
if a % 2 != 0:
    print("0 0")
elif a % 2 == 0 and a % 4 != 0:
    print(a//4 + 1, a//2)
else:
    print(a//4, a//2)

```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240922165321919](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20240922165321919.png)



### 50A. Domino piling

greedy, math, 800, http://codeforces.com/problemset/problem/50/A



思路：面积偶数铺满，奇数减一



##### 代码

```python
lst = input().split()
pro = int(lst[0]) * int(lst[1])
print(pro//2)

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240922170015778](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20240922170015778.png)



### 1A. Theatre Square

math, 1000, https://codeforces.com/problemset/problem/1/A



思路：分别算长边和宽边需要的个数再相乘



##### 代码

```python
lst = input().split()
if int(lst[0])%int(lst[2]) == 0:
    b = int(lst[0])//int(lst[2])
else:
    b = int(lst[0])//int(lst[2])+1
if int(lst[1])%int(lst[2]) == 0:
    c = int(lst[1])//int(lst[2])
else:
    c = int(lst[1])//int(lst[2])+1
print(b*c)

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240922165942873](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20240922165942873.png)



### 112A. Petya and Strings

implementation, strings, 1000, http://codeforces.com/problemset/problem/112/A



思路：字符串直接比大小



##### 代码

```python
str1 = input().lower()
str2 = input().lower()
if str1 < str2:
    print(-1)
elif str1 > str2:
    print(1)
else:
    print(0)

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==



![image-20240922170055665](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20240922170055665.png)

### 231A. Team

bruteforce, greedy, 800, http://codeforces.com/problemset/problem/231/A



思路：对每行求和，如果大于1就答案加1



##### 代码

```python
a = int(input())
result = 0
for i in range(a):
    lst_i = input().split()
    if sum(int(num) for num in lst_i)>1:
        result += 1
print(result)

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==



![image-20240922170122178](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20240922170122178.png)

## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。==

我暑假在B站上学了一点python的基础课，但一直苦于没有合适的练习题，在leetcode上找的题都感觉好难，无从下手。因此在进群发现老师每天会给补充题时特别惊喜，感觉完美地解决了我的困难。感觉我们班的学习氛围特别好，对我这种小白也很友好。我所在的院系没有推荐，因此能够选上闫老师的课特别幸运（31/193），也很感谢老师扩名额！因为31号才进群，所以落下了一些选做题，现在在努力赶上进度。最开始看到题时毫无思路，语法看了就忘；现在基本能够形成思路并写成代码，语法也渐渐掌握。虽然常常比答案写得复杂，但在跟答案对比或是询问AI的过程中也积累了一些很不错的思路。



