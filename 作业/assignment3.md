# Assign #3: Oct Mock Exam暨选做题目满百

Updated 1537 GMT+8 Oct 10, 2024

2024 fall, Complied by Hongfei Yan==（请改为同学的姓名、院系）==彭凌越，光华管理学院



**说明：**

1）Oct⽉考： AC6==（请改为同学的通过数）== AC4。考试题⽬都在“题库（包括计概、数算题目）”⾥⾯，按照数字题号能找到，可以重新提交。作业中提交⾃⼰最满意版本的代码和截图。

2）请把每个题目解题思路（可选），源码Python, 或者C++/C（已经在Codeforces/Openjudge上AC），截图（包含Accepted, 学号），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、作业评论有md或者doc。

4）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### E28674:《黑神话：悟空》之加密

http://cs101.openjudge.cn/practice/28674/



思路：ASCII表判断偏移后是否在范围内

用时约10min



代码

```python
n = int(input())%26
s = input()
ans = ''
for _ in s:
    if 'a'<=_<='z':
        if 'a'<=chr(ord(_)-n)<='z':
            _ = chr(ord(_)-n)
        else:
            _= chr(ord(_)-n+26)
    else:
        if 'A'<=chr(ord(_)-n)<="Z":
            _ = chr(ord(_) - n)
        else:
            _= chr(ord(_)-n+26)
    ans += _
print(ans)

```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20241011140546820](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241011140546820.png)



### E28691: 字符串中的整数求和

http://cs101.openjudge.cn/practice/28691/



思路：把前两位转化为int类型相加（但是刚开始没发现输入只有一行致错）

用时约5min



代码

```python
lst = input().split()
a, b= int(lst[0][:2]),int(lst[1][:2])
print(a+b)

```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20241011140810322](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241011140810322.png)



### M28664: 验证身份证号

http://cs101.openjudge.cn/practice/28664/



思路：通过列表索引对应结果

用时约13min

代码

```python
n = int(input())
xishu = [7,9,10,5,8,4,2,1,6,3,7,9,10,5,8,4,2]
res = [1,0,'X',9,8,7,6,5,4,3,2]
for i in range(n):
    s = input()
    c = 0
    for _ in range(17):
        c += int(s[_:_+1])*xishu[_]
    c = c%11
    if s[17:]=='X':
        if res[c] == 'X':
            print('YES')
        else:
            print('NO')
    else:
        if res[c] == int(s[17:]):
            print('YES')
        else:
            print('NO')

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20241011140844333](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241011140844333.png)



### M28678: 角谷猜想

http://cs101.openjudge.cn/practice/28678/



思路：先计算结果再单个字符逐个打印

用时约5min



代码

```python
n = int(input())
while n != 1:
    if n % 2 ==1:
        c = n*3+1
        print(str(n)+'*'+'3'+'+'+'1'+"="+str(c))
        n = c
    else:
        c = n//2
        print(str(n)+'/'+'2'+'='+str(c))
        n = c
if n == 1:
    print('End')

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20241011140917669](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241011140917669.png)



### M28700: 罗马数字与整数的转换

http://cs101.openjudge.cn/practice/28700/



思路：先用isdigit()判断输入是否是数字，再用字典和列表转化

用时1h+，开始忘记字典无序，后来列表逆序索引写错了



##### 代码

```python
n = input()
dic = [('IV',4),('IX',9),('XL',40),('XC',90),('CD',400),('CM',900)]
d = [('I',1),('IV',4),('V',5),('IX',9),('X',10),('XL',40),('L',50),('XC',90),('C',100),('CD',400),('D',500),('CM',900),('M',1000)]
if n[:1].isdigit():
    n = int(n)
    ans = ''
    for i in range(-1, -14, -1):
        a = n // d[i][1]
        ans += d[i][0] * a
        n -= a * d[i][1]
    print(ans)
else:
    di = {'I':1,'V':5,'X':10,'L':50,'C':100,'D':500,'M':1000}
    res = 0
    for i in range(6):
        if dic[i][0] in n:
            res += dic[i][1]
            n = n.replace(dic[i][0],'')
    for letter in n:
        res += di[letter]
    print(res)

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20241011141827003](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241011141827003.png)



### *T25353: 排队 （选做）

http://cs101.openjudge.cn/practice/25353/



思路：类似分组，每一组每个数一定和该组其他数差别不超过d，排序后再合并（用*解包）；用deque比list快

用时1h+

代码

```python
from collections import deque
n, d = map(int, input().split())
deq = deque(int(input()) for i in range(n))
res = []
while deq:
    lst = []
    max_h = deq[0]
    min_h = deq[0]
    for i in range(len(deq)):
        height = deq.popleft()
        if abs(height - min_h)<=d and abs(height - max_h)<=d:
            lst.append(height)
        else:
            deq.append(height)
        if min_h > height:
            min_h = height
        if max_h < height:
            max_h = height
    res += sorted(lst)
print(*res,sep='\n')

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20241011212954038](C:\Users\28566\AppData\Roaming\Typora\typora-user-images\image-20241011212954038.png)



## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。==

有些语法还是不够熟练，在代码较长的题目中就会出错。上午12分钟跑引发鼻炎，考试的时候一直难受，还看错了题，最后只AC了4道。有些代码写得太繁琐了，导致WA了以后也难以检查出错误。最后一道题感觉好复杂，自己做完全没有思路。以后在每日选做中尽量对着答案简化一下自己的代码，多积累一些算法。

CF上的每日选做都尽量跟上了，OJ还差几题，争取这周末做完。









