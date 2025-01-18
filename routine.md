包含Openjudge和LeetCode上的题目

#### Openjudge

hangover http://cs101.openjudge.cn/2024fallroutine/01003/

```python
import math
while True:
    a = float(input())
    if math.isclose(a, 0.00):
        break
    else:
        found = False
        for i in range(275):
            res = 0
            for n in range(1, i+1):
                res += 1/(n+1)
                if res >= a:
                    print(str(i)+" card(s)")
                    found = True
                    break
            if found:
                break
```

maya calendar http://cs101.openjudge.cn/2024fallroutine/01008/

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

装箱问题 http://cs101.openjudge.cn/2024fallroutine/01017/

```python
import math
r = [0,5,3,1]
while True:
    a,b,c,d,e,f= map(int, input().split())
    if a+b+c+d+e+f==0:
        break
    else:
        count = f
        count += e+d+math.ceil(c/4)
        s = 5 * d + r[c%4]
        if b > s:
            count += math.ceil((b - s) / 9)
        s = count * 36 - (36 * f + 25 * e + 16 * d + 9 * c + 4 * b)
        if a > s:
            count += math.ceil((a - s) / 36)
        print(count)
#第一次做的时候分c,d,e,f剩余格子一个一个考虑，太麻烦了；先考虑b再考虑a会方便很多
```

number sequence http://cs101.openjudge.cn/2024fallroutine/01019/

```python
import bisect
sequence = ""
s = 0
ss = 0
sums = []
for j in range(1, 33000):
    sequence += str(j)
    s += len(str(j))
    ss += s
    sums.append(ss)
a = int(input())
for _ in range(a):
    x = int(input())

    if x == 1:
        print(1)
    else:
        i = bisect.bisect_left(sums, x)
        res = x - sums[i - 1] - 1
        seq = sequence[res]
        print(seq)
```

cipher http://cs101.openjudge.cn/2024fallroutine/01026/



drunk jailerhttp://cs101.openjudge.cn/2024fallroutine/01218/

```
import math
n = int(input())
for i in range(n):
    count = 0
    a = int(input())
    for k in range(1,a+1):
        if int(math.sqrt(k))**2==k:
            count+=1
    print(count)
```

radarhttp://cs101.openjudge.cn/2024fallroutine/01328/

```
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

antshttp://cs101.openjudge.cn/2024fallroutine/01852/

```
n = int(input())
for i in range(n):
    min_time = []
    max_time = []
    l, k = map(int, input().split())
    lst = list(map(int,input().split()))
    for m in lst:
        min_t = min(m, l-m)
        min_time.append(min_t)
    min_t = max(min_time)
    for q in lst:
        max_t = max(q,l-q)
        max_time.append(max_t)
    max_t = max(max_time)
    print(str(min_t)+' '+str(max_t))
```

大小写互换http://cs101.openjudge.cn/2024fallroutine/02689/

```
s = input()
b = ord("a") - ord("A")
res = ""
for i in s:
    if "a" <= i <= "z":
        res += chr(ord(i) - b)
    elif "A" <= i <= "Z":
        res += chr(ord(i) + b)
    else:
        res += i
print(res)
```

与七无关的数http://cs101.openjudge.cn/2024fallroutine/02701/

```
a = int(input())
res = 0
for i in range(a+1):
    if i %7 != 0 and "7" not in str(i):
       res += i ** 2
print(res)
```

约瑟夫http://cs101.openjudge.cn/2024fallroutine/02746/

```
def leader(n,m):
    if n == 1:
        return n
    return (leader(n-1,m)+m-1)%n+1
while True:
    n, m = map(int,input().split())
    if n+m==0:
        break
    print(leader(n,m))
```

斐波那契http://cs101.openjudge.cn/2024fallroutine/02753/

```
lst = [1]*20
for i in range(2, 20):
    lst[i]=lst[i-2]+lst[i-1]
n = int(input())
for k in range(n):
    print(lst[int(input())-1])
```

数字三角形http://cs101.openjudge.cn/2024fallroutine/02760/

```
N = int(input())
tri = []
for _ in range(N):
    tri.append([int(i) for i in input().split()])
dp = [[0]*N for _ in range(N)]
for j in range(N):
    dp[N-1][j] = tri[N-1][j]
for i in range(N-2, -1, -1):
    for j in range(i+1):
        dp[i][j] = max(dp[i+1][j], dp[i+1][j+1]) + tri[i][j]
print(dp[0][0])
```

最大子矩阵http://cs101.openjudge.cn/2024fallroutine/02766/

```
def max_submatrix(matrix):
    def kadane(arr):
        max_end_here = max_so_far = arr[0]
        for x in arr[1:]:
            max_end_here = max(x, max_end_here + x)
            max_so_far = max(max_so_far, max_end_here)
        return max_so_far

    rows = len(matrix)  # 获取矩阵的行数
    cols = len(matrix[0])  # 获取矩阵的列数（假设矩阵是矩形的）
    max_sum = float('-inf')  # 初始化最大和为负无穷大

    # 遍历所有可能的左边界
    for left in range(cols):
        temp = [0] * rows  # 初始化临时的一维数组，用来累积每一行的元素和
        
        # 遍历从当前左边界开始的所有可能的右边界
        for right in range(left, cols):
            # 累加从left到right的每一行的元素值到temp中
            for row in range(rows):
                temp[row] += matrix[row][right]
            
            # 应用Kadane算法计算当前固定左右边界的最大和，并更新max_sum
            max_sum = max(max_sum, kadane(temp))

    return max_sum  # 返回找到的最大和
n = int(input())
nums = []
while len(nums) < n * n:
    nums.extend(input().split())
matrix = [list(map(int, nums[i * n:(i + 1) * n])) for i in range(n)]
print(max_submatrix(matrix))
```

holiday hotelhttp://cs101.openjudge.cn/2024fallroutine/02783/

```
while True:
    n = int(input())
    if n == 0:
        break
    res = []
    for i in range(n):
        res.append(tuple(map(int,input().split())))
    res.sort(key=lambda x:(x[0],x[1]))
    ans = 1
    cost = res[0][1]
    for k in range(1,n):
        if res[k][1]<cost:
            ans += 1
            cost = res[k][1]
    print(ans)
#sort方式
```

pell数列http://cs101.openjudge.cn/2024fallroutine/02786/

```
lst = [1]*1000000
lst[1]=2
for i in range(2, 1000000):
    lst[i]=(lst[i-2]+2*lst[i-1])%32767
n = int(input())
for k in range(n):
    print(lst[int(input())-1])
#取模
```

集合加法http://cs101.openjudge.cn/2024fallroutine/02792/

```
#5219ms
n = int(input())
for i in range(n):
    count = 0
    s = int(input())
    a = int(input())
    lst_a = list(map(int, input().split()))
    b = int(input())
    lst_b = list(map(int, input().split()))
    for k in lst_a:
        c = lst_b.count(s-k)
        count += c
    print(count)
```

```
#47ms
from collections import Counter
def calculate_pairs(arr1, arr2, target_sum):
    counter1 = Counter(arr1)
    counter2 = Counter(arr2)
    ans = 0
    for item in counter1:
        if target_sum - item in counter2:
            ans += counter1[item] * counter2[target_sum - item]
    return ans
for _ in range(int(input())):
    s = int(input())
    input()
    l1 = list(map(int, input().split()))
    input()
    l2 = list(map(int, input().split()))
    ans = calculate_pairs(l1, l2, s)
    print(ans)
```

```
#50ms
from collections import Counter
n = int(input())
for i in range(n):
    count = 0
    s = int(input())
    a = int(input())
    lst_a = list(map(int, input().split()))
    b = int(input())
    lst_b = list(map(int, input().split()))
    counter = Counter(lst_b)
    for k in lst_a:
        c = counter[s-k]
        count += c
    print(count)
```

校门外的树http://cs101.openjudge.cn/2024fallroutine/02808/

```
L, M = map(int, input().split())
lst = [1]*(L+1)
for i in range(M):
    a, b = map(int, input().split())
    for n in range(a, b+1):
        lst[n] = 0
print(lst.count(1))
#第一次做的时候没考虑区域重叠
```

完美立方http://cs101.openjudge.cn/2024fallroutine/02810/

```
n = int(input())
for a in range(6,n+1):
    for b in range(2,a):
        for c in range(b,a):
            for d in range(c,a):
                if a**3 == b**3+c**3+d**3:
                    print("Cube = {}, Triple = ({},{},{})".format(a,b,c,d))
                    break
```

拦截导弹http://cs101.openjudge.cn/2024fallroutine/02945/

```
n = int(input())
def missile(n,lst):
    dp = [1]*n
    for i in range(1,n):
        for j in range(i):
            if lst[i]<=lst[j]:
                dp[i]=max(dp[i],dp[j]+1)
    return max(dp)


lst = list(map(int,input().split()))
print(missile(n,lst))
```

大整数加法http://cs101.openjudge.cn/2024fallroutine/02981/

```
a = int(input())
b = int(input())
print(a+b)
```

登山http://cs101.openjudge.cn/2024fallroutine/02995/

```
n = int(input())
*h, = map(int, input().split())

dp = [1]*n

for i in range(1, n) :
    for j in range(i):
        if h[j] < h[i]:
            dp[i] = max(dp[i], dp[j] + 1)


*rev_h, = reversed(h)
rdp = [1]*n

for i in range(1, n) :
    for j in range(i):
        if rev_h[j] < rev_h[i]:
            rdp[i] = max(rdp[i], rdp[j] + 1)

u = 0
zip_dp = zip(dp, list(reversed(rdp)))
*u, = map(lambda x: x[0]+x[1], zip_dp)

print(max(u) - 1)
```

验证哥德巴赫http://cs101.openjudge.cn/2024fallroutine/03143/

```
a = int(input())
lst = []
for i in range(2,1999):
    found = False
    for j in range(2,max(i//2, 3)):
        if i % j == 0:
            found = True
            break
    if found is False:
        lst.append(i)
if a <= 5 or a % 2 == 1:
    print("Error!")
else:
    for b in lst:
        if b <= a - b and (a - b) in lst:
            print(f"{a}={b}+{a - b}")

#for b, c in lst: 循环错误：lst 存储的是单个整数，而不是成对的 (b, c)。因此，这里应该使用单个变量来遍历 lst。
#第一次建立素数列表时逻辑写错了
#for 循环不能用and ;while循环可以
#打印格式错误：在 print(a = b + c) 中，a = b + c 是赋值语句而非字符串格式化。正确的做法是使用 f-string 或者其他字符串格式化方法。
```

最大公约数http://cs101.openjudge.cn/2024fallroutine/03248/

```
#223ms
while True:
    try:
        lst = input().split()
        lst = list(map(int, lst))
        a = min(lst[0], lst[1])
        b = max(lst[0], lst[1])
        for i in range(a+1, 0, -1):
            if a % i == 0 and b % i == 0:
                print(i)
                break
    except:
        break
#第四行不能用[]
#try,except
#range要包含1
```

```
#32ms
def gcd(x, y):
    while(y):
        x, y = y, x % y
    return x

while True:
    try:
        # 读取输入并转换为整数列表
        lst = input().split()
        lst = list(map(int, lst))
        
        # 获取两个数
        a, b = lst[:2]
        
        # 计算最大公约数
        result = gcd(max(a, b), min(a, b))
        
        # 输出结果
        print(result)
    except EOFError:
        # 当没有更多输入时，退出循环
        break
#while(y):  # 当 y 不为零时继续循环
#x, y = y, x % y  # 更新 x 和 y 的值
#return x  # 当 y 变为 0 时，返回 x 作为最大公约数
```

约瑟夫2http://cs101.openjudge.cn/2024fallroutine/03253/

```
def circ(n,p,m):
    res = []
    if n == 1:
        return [1]
    kid = list(range(1,n+1))
    index = p-1
    while len(kid)>0:
        index = (index+m-1)%len(kid)
        res.append(kid.pop(index))
    return res
while True:
    n,p,m=map(int,input().split())
    if n+p+m==0:
        break
    ans = circ(n,p,m)
    print(','.join(map(str,ans)))
```

邮箱验证http://cs101.openjudge.cn/2024fallroutine/04015/

```
while True:
    try:
        a = input()
        if not a:
            break
        if a.count('@') != 1 or a[0] =='@' or a[0] == '.' or a[-1] == '.' or '@.' in a or '.@' in a:
            print('NO')
        else:
            b = a.find('@')
            if '.' in a[b:]:
                print("YES")
            else:
                print('NO')
    except EOFError:
        break
```

圣诞老人http://cs101.openjudge.cn/2024fallroutine/04110/

```
n, w = map(int, input().split())
dic = dict()
ans = 0
for i in range(n):
    a, b = map(int,input().split())
    c = a/b
    if c not in dic:
        dic[c]=[a,b]
    else:
        dic[c]=[dic[c][0]+a,dic[c][1]+b]
di = sorted(dic,reverse=True)#sort的是前面的浮点数
for k in di:
    if w >= dic[k][1]:
        ans+=dic[k][0]
        w -= dic[k][1]
    else:
        ans += w/dic[k][1]*dic[k][0]
        break
print(f"{ans:.1f}",end='\n')
#k是浮点数会报错，而列表索引必须是整数或者切片
```

变换迷宫http://cs101.openjudge.cn/2024fallroutine/04129/

```
from collections import deque

def bfs(x, y):
    visited = {(0, x, y)}
    dx = [0, 0, 1, -1]
    dy = [1, -1, 0, 0]
    queue = deque([(0, x, y)])
    while queue:
        time, x, y = queue.popleft()
        for i in range(4):
            nx, ny = x + dx[i], y + dy[i]
            te = (time + 1) % k
            if 0 <= nx < r and 0 <= ny < c and (te, nx, ny) not in visited:
                now = ma[nx][ny]
                if now == 'E':
                    return time + 1
                elif now != '#' or te == 0:
                    queue.append((time + 1, nx, ny))
                    visited.add((te, nx, ny))
    return 'Oop!'


t = int(input())
for _ in range(t):
    r, c, k = map(int, input().split())
    ma = [list(input()) for _ in range(r)]
    for i in range(r):
        for j in range(c):
            if ma[i][j] == 'S':
                print(bfs(i, j))
```

质数和积http://cs101.openjudge.cn/2024fallroutine/04138/

```
import math
a = int(input())
lst = [2]
for i in range(3,6000):
    found = False
    for k in range(2,max(int(math.sqrt(i))+1,3)):
        if i % k ==0:
            found = True
            break
    if not found:
        lst.append(i)
for m in range(a//2, 1, -1):
    if m in lst and a-m in lst:
        print(m*(a-m))
        break
```

数字方格http://cs101.openjudge.cn/2024fallroutine/04146/

```
n = int(input())
res = []
for a in range(n,-1,-1):
    for b in range(n,-1,-1):
        for c in range(n,-1,-1):
            if (a+b+c)%5==0 and (a+b)%2==0 and (b+c)%3==0:
                res.append(a+b+c)
                break
        
res = max(res)
print(res)
```

生理周期http://cs101.openjudge.cn/2024fallroutine/04148/

```
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

文字排版http://cs101.openjudge.cn/2024fallroutine/06374/

```
int(input())
f = input().split()
res = []
str_1 = f[0] + ' '
for i in f[1:]:
    if len(str_1) + len(i) <= 80:
        str_1 += i + " "
    else:
        res.append(str_1.rstrip())
        str_1 = i + ' '
else:
    res.append(str_1.rstrip()) 
print("\n".join(res))
```

核电站http://cs101.openjudge.cn/2024fallroutine/09267/

```
n, m = map(int, input().split())
DP = [0] * 60
DP[0] = 1 #DP[i]是第i个位置的方案数

for i in range(1, n + 1):
    if i < m: #达不到连续放置m个的情况
        DP[i] = DP[i - 1] * 2  # 从第1个到第m-1个，方案都可以选择放/不放
    elif i == m: 
        DP[i] = DP[i - 1] * 2 - 1
    else:#i>m
        DP[i] = DP[i - 1] * 2 - DP[i - m - 1]
print(DP[n])
```

编码字符串http://cs101.openjudge.cn/2024fallroutine/12556/

```
s = input().lower()
lst = []
ori = s[0]
count = 1
for i in range(1, len(s)):
    if s[i] == ori:
        count += 1
    else:
        lst.append("("+ori+"," + str(count) + ")")
        ori = s[i]
        count = 1
else:
    lst.append("("+ori+"," + str(count) + ")")
print("".join(lst))
```

矩阵运算http://cs101.openjudge.cn/2024fallroutine/18161/

```
x=[];y = [];z=[]
a,b= map(int,input().split())
for _ in range(a):
    x.append(list(map(int,input().split())))

c,d=map(int,input().split())
for _ in range(c):
    y.append(list(map(int,input().split())))

e,f=map(int,input().split())
for _ in range(e):
    z.append(list(map(int,input().split())))

if a!=e or d!=f or b!=c:
    print('Error!')
else:
    for i in range(e):
        for j in range(f):
            z[i][j]+=sum(x[i][p]*y[p][j]for p in range(b))
    for i in range(e):
        print(' '.join(map(str, z[i])))
```

军备竞赛http://cs101.openjudge.cn/2024fallroutine/18211/

```
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

24点http://cs101.openjudge.cn/2024fallroutine/18223/

```
n = int(input())
for i in range(n):
    found = False
    a,b,c,d = map(int,input().split())
    for m in [a, -a]:
        for n in [b,-b]:
            for p in [c,-c]:
                for q in [d,-d]:
                    if m+n+p+q == 24:
                        found = True
                        break
                if found:
                    break
            if found:
                break
        if found:
            break
    print('YES' if found else 'NO')
```

星期几http://cs101.openjudge.cn/2024fallroutine/19944/

```
n = int(input())
for i in range(n):
    a = input()
    y = int(a[2:4])
    m = int(a[4:6])
    if m < 3:
        y -= 1
        m += 12
    c = int(a[:2])
    d = int(a[6:8])
    if y == -1 and m >= 13:
        y = 99
        c -= 1
    w = (y+y//4+c//4-2*c+(13 *(m + 1) // 5+d-1))%7
    Day = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday','Saturday']
    print(Day[w])
#用列表，不要用7个if
```

提取实体http://cs101.openjudge.cn/2024fallroutine/19949/

```
T = int(input())
ans = 0
while T>0:
    T -= 1
    ans += (input().replace('### ###', '')).count('###') // 2
print(ans)
```

how old are youhttp://cs101.openjudge.cn/2024fallroutine/21459/

```
x = int(input())
while x != 1:
    if x % 2 == 0:
        y = x // 2
        print("{}/2={}".format(x, y))
        x = y
    else:
        y = x*3+1
        print("{}*3+1={}".format(x, y))
        x = y
```

数学密码http://cs101.openjudge.cn/2024fallroutine/21532/

```
a = int(input())
found = False
for i in range(6,a//2+1):
    if a % i == 0:
        print(a//i)
        found = True
        break
if not found:
    print(1)
```

排队做实验http://cs101.openjudge.cn/2024fallroutine/21554/

```
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

小偷背包http://cs101.openjudge.cn/2024fallroutine/23421/

```
import math
n,b=map(int,input().split())
a=list(map(int,input().split()))
c = list(map(int,input().split()))


def pack(i,s):
    if s<0:
        return -math.inf
    if i == len(a):
        return 0
    return max(pack(i+1,s),a[i]+pack(i+1,s-c[i]))


print(pack(0,b))
```

小朋友春游http://cs101.openjudge.cn/2024fallroutine/23554/

```
n = int(input())
s = list(map(int,input().split()))
ans = []
res = []
for i in range(1,n+1):
    if i not in s:
        ans.append(i)
    else:s.remove(i)
ans.sort()
s.sort()
print(" ".join(map(str,ans)))
print(' '.join(map(str,s)))
```

数论http://cs101.openjudge.cn/2024fallroutine/23564/

```
from math import sqrt
n = int(input())
pFact, limit, check, num = [], int(sqrt(n)) + 1, 2, n
for check in range(2, limit):
    while num % check == 0:
        pFact.append(check)
        num /= check
if num > 1:
    pFact.append(num)
s = set(pFact)
a = len(pFact)
b = len(s)
if a != b:
    print(0)
else:
    if a % 2 == 1:
        print(-1)
    else:
        print(1)
```

二进制回文整数http://cs101.openjudge.cn/2024fallroutine/25538/

```
a = bin(int(input()))[2:]
if a == a[::-1]:
    print("Yes")
else:
    print("No")
#切片时两个：不能省
```

简单数学题http://cs101.openjudge.cn/2024fallroutine/27273/

```
n = int(input())
for i in range(n):
    k = -1
    a = int(input())
    for m in range(a):
        if 2**m <= a < 2**(m+1):
            k = m
            break
    if k != -1:
        res = -2**(k+2) + 2 + (1 + a)*a//2
        print(res)
#初始化k为-1，用于标记是否找到了符合条件的k,也能避免产生k未定义的情况
```

世界杯http://cs101.openjudge.cn/2024fallroutine/27104/

```
n = int(input())
ls = list(map(int, input().split()))
ends = [0]*n		
for i in range(n):
    if i - ls[i] > 0:
        ends[i - ls[i]] = i + ls[i]
    else:
        ends[0] = max(ends[0], i + ls[i])		
count = 1
l = r = ends[0]
for i in range(1, n):
    r = max(r, ends[i])
    if i >= l + 1:
        l = r
        count += 1
print(count)
```

健身房http://cs101.openjudge.cn/routine/21458/

```
t,n=map(int,input().split())
lst = []
for i in range(n):
    lst.append(list(map(int,input().split())))
dp=[0]+[-1]*t
for j in range(n):
    for i in range(t,-1,-1):

        if i>=lst[j][0] and dp[i-lst[j][0]]!=-1:
            dp[i]=max(dp[i],dp[i-lst[j][0]]+lst[j][1])
if dp[t]==-1:
    print(-1)
else:
    print(dp[t])
```

给植物浇水http://cs101.openjudge.cn/practice/27301/

```
n,a,b=map(int,input().split())
lst=list(map(int,input().split()))
x=1
cnt=0
y=n-2
a0=a-lst[0]
b0=b-lst[-1]
while x<=y:
    if x<y:
        if a0>=lst[x]:
            a0-=lst[x]
        else:
            a0=a-lst[x]
            cnt+=1
        x+=1
        if b0>=lst[y]:
            b0-=lst[y]
        else:
            b0=b-lst[y]
            cnt+=1
        y-=1
    else:
        if a0<lst[x] and b0<lst[x]:
            cnt+=1
        break
print(cnt)
```

体育游戏跳房子http://cs101.openjudge.cn/practice/27237/

```
import heapq
while True:
    n,m=map(int,input().split())
    if m+n==0:
        break
    queue=[]
    lst=[]
    s=''
    inq=set()
    heapq.heappush(queue,(0,'',n))
    inq.add(n)
    flag = False
    min_step=25
    while queue:
        step,s1,x=heapq.heappop(queue)
        inq.add(x)
        if step > min_step:
            break
        if x==m:
            min_step=min(step,min_step)
            lst.append(s1)
            flag=True

        x1=x*3
        if x1 not in inq:
            inq.add(x1)
            heapq.heappush(queue,(step+1,s1+'H',x1))
        x2=x//2
        if x2>=1 and x2 not in inq:
            inq.add(x2)
            heapq.heappush(queue,(step+1,s1+'O',x2))
    print(min_step)
    print(min(lst))
```

积木http://cs101.openjudge.cn/practice/27310/

```
from itertools import permutations
n=int(input())
a1=input()
b1=input()
c1=input()
d1=input()
lst=[]
for a in range(6):
    for b in range(6):
        for c in range(6):
            for d in range(6):
                lst+=list(permutations([a1[a],b1[b],c1[c],d1[d]],2))
                lst+=list(permutations([a1[a], b1[b], c1[c], d1[d]], 3))
                lst+=list(permutations([a1[a], b1[b], c1[c], d1[d]], 4))
                lst+=list(permutations([a1[a], b1[b], c1[c], d1[d]], 1))
for i in range(n):
    if tuple(input()) in lst:
        print('YES')
    else:
        print('NO')
```

字符串提炼http://cs101.openjudge.cn/practice/27274/

```
import math
s=input()
n=len(s)
m=math.floor(math.log(n,2))
s1=''
a,b=0,m
while a<b:
    s1+=s[2**a-1]+s[2**b-1]
    a+=1
    b-=1
if a==b:
    s1+=s[2**a-1]
print(s1)
```

最大联通区域面积http://cs101.openjudge.cn/practice/18160/

```
def dfs(x,y):
    res = 0
    stack=[(x,y)]
    while stack:
        x,y = stack.pop()
        if ma[x][y]!='W':
            continue
        ma[x][y]='.'
        res+=1
        for dx,dy in dir:
            nx,ny=x+dx,y+dy
            if 0<=nx<n and 0<=ny<m and ma[nx][ny]=='W':
                stack.append((nx,ny))

    ans.append(res)
    return ans,ma
t = int(input())

dir=[(-1, -1), (-1, 0), (-1, 1), (0, -1), (0, 1), (1, -1), (1, 0), (1, 1)]
for i in range(t):
    ans = []
    n,m=map(int,input().split())
    ma=[]
    for j in range(n):
        ma.append(list(input()))
    for x in range(n):
        for y in range(m):
            if ma[x][y]=='W':
                dfs(x,y)
    print(max(ans) if ans else 0)
```

采药http://cs101.openjudge.cn/practice/02773/

```
t,m=map(int,input().split())
dp=[0]*(t+1)
for i in range(m):
    a,b=map(int,input().split())
    for j in range(t,-1,-1):
        if j>=a:
            dp[j]=max(dp[j],dp[j-a]+b)
print(dp[-1])
```

滑雪http://cs101.openjudge.cn/practice/01088/

```
r, c = map(int, input().split())
ma = [list(map(int, input().split())) for _ in range(r)]
dp = [[-1]*c for _ in range(r)]
dx = [-1, 0, 1, 0]
dy = [0, 1, 0, -1]
from functools import lru_cache
@lru_cache(maxsize=None)
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

公共子序列http://cs101.openjudge.cn/practice/02806/

```
while True:
    try:
        a, b = input().split()
    except EOFError:
        break
    
    alen = len(a)
    blen = len(b)
    
    dp = [[0]*(blen+1) for i in range(alen+1)]

    for i in range(1, alen+1):
        for j in range(1, blen+1):
            if a[i-1]==b[j-1]:
                dp[i][j] = dp[i-1][j-1] + 1
            else:
                dp[i][j] = max(dp[i-1][j], dp[i][j-1])


    print(dp[alen][blen])
```

NBA门票http://cs101.openjudge.cn/practice/20089/

```
import math
n = int(input())
price = [50,100,250,500,1000,2500,5000]
lst = list(map(int,input().split()))
dp = [0]+[-1]*n
for i in range(7):
    num = lst[i]+1
    lim = int(math.log(num,2))
    rest = num-(1<<lim)
    for k in range(lim):
        for j in range(n,-1,-50):
            if j>=price[i]*(1<<k) and dp[j-price[i]*(1<<k)]!=-1:
                if dp[j]!=-1:
                    dp[j]=min(dp[j],dp[j-price[i]*(1<<k)]+(1<<k))
                else:
                    dp[j]=dp[j-price[i]*(1<<k)]+(1<<k)
    if rest >0:
        for j in range(n,-1,-50):
            if j>=price[i]*rest and dp[j-price[i]*rest]!=-1:
                if dp[j]!=-1:
                    dp[j]=min(dp[j],dp[j-price[i]*rest]+rest)
                else:
                    dp[j]=dp[j-price[i]*rest]+rest

if dp[n]!=-1:
    print(dp[n])
else:
    print('Fail')
```

Coinshttp://cs101.openjudge.cn/practice/01742/

```
import math
while True:
    n, m = map(int, input().split())
    if n == 0 and m == 0:
        break
    ls = list(map(int, input().split()))
    w = (1 << (m + 1)) - 1                 
    result = 1
    for i in range(n):
        number = ls[i+n] + 1                
        limit = int(math.log(number, 2))    
        rest = number - (1 << limit)        
        for j in range(limit):
            result = (result | (result << (ls[i] * (1 << j)))) & w
        if rest > 0:
            result = (result | (result << (ls[i] * rest))) & w
    print(bin(result).count('1') - 1)
```

piggy_bankhttp://cs101.openjudge.cn/practice/01384/

```
INF = float("inf")

TC = int(input())
for _ in range(TC):
    E, F = map(int, input().split())
    N = int(input())

    amount = F - E
    dp = [0] + [INF] * amount

    for _ in range(N):
        p, w = map(int, input().split())
        if w <= amount:  # 如果硬币的重量超过了背包容量，则跳过此硬币
            for j in range(w, amount + 1):
                if dp[j-w] != INF:
                    dp[j] = min(dp[j], dp[j-w] + p)
                    if j == amount and dp[j] != INF:  
                        break

    if dp[-1] != INF:
        print(f"The minimum amount of money in the piggy-bank is {dp[-1]}.")
    else:
        print("This is impossible.")
```

河中跳房子http://cs101.openjudge.cn/practice/08210/

```
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

熄灯http://cs101.openjudge.cn/practice/02811/

```
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
                                print(" ".join(repr(y) for y in [B[i][1],B[i][2],B[i][3],B[i][4],B[i][5],B[i][6] ]))
```

最大整数http://cs101.openjudge.cn/practice/27373/

```
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

螃蟹采蘑菇http://cs101.openjudge.cn/practice/25572/

```
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

假币http://cs101.openjudge.cn/practice/02692/

```
n = int(input())
letter = ['A','B','C','D','E','F','G','H','I','J','K','L']
for i in range(n):
    good = set()
    light = set()
    heavy = set()
    fake_pro = set()
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

最大上升子序列和http://cs101.openjudge.cn/practice/03532/

```
input()
a = [int(x) for x in input().split()]
n = len(a)
dp = [0]*n
for i in range(n):
    dp[i] = a[i]
    for j in range(i):
        if a[j] < a[i]:
            dp[i] = max(dp[j]+a[i], dp[i])
print(max(dp))
```

走山路http://cs101.openjudge.cn/practice/20106/

```
from heapq import heappop, heappush

def bfs(x1, y1):
    q = [(0, x1, y1)]
    visited = set()
    while q:
        t, x, y = heappop(q)
        if (x, y) in visited:
          continue
        visited.add((x, y))
        if x == x2 and y == y2:
            return t
        for dx, dy in dir:
            nx, ny = x+dx, y+dy
            if 0 <= nx < m and 0 <= ny < n and \
                    ma[nx][ny] != '#' and (nx, ny) not in visited:
                nt = t+abs(int(ma[nx][ny])-int(ma[x][y]))
                heappush(q, (nt, nx, ny))
    return 'NO'


m, n, p = map(int, input().split())
ma = [list(input().split()) for _ in range(m)]
dir = [(1, 0), (-1, 0), (0, 1), (0, -1)]
for _ in range(p):
    x1, y1, x2, y2 = map(int, input().split())
    if ma[x1][y1] == '#' or ma[x2][y2] == '#':
        print('NO')
        continue
    print(bfs(x1, y1))
```

堆猪http://cs101.openjudge.cn/practice/22067/

```
lst = []
m = []
while True:
    try:
        s = input().split()
        if s[0] == "pop":
            if lst:
                lst.pop()
                if m:
                    m.pop()
        elif s[0] == "min":
            if m:
                print(m[-1])
        else:
            t = int(s[1])
            lst.append(t)
            if not m:
                m.append(t)
            else:
                k = m[-1]
                m.append(min(k, t))
    except:
        break
```

洋葱http://cs101.openjudge.cn/practice/25570/

```
n = int(input())
ma=[]
ans =[]
for i in range(n):
    ma.append(list(map(int,input().split())))
for k in range(n//2):
    res = sum(ma[k][k:n-k])+sum(ma[n-k-1][k:n-k])
    for u in range(k+1,n-k-1):
        res+=ma[u][k]+ma[u][n-k-1]
    ans.append(res)
if n%2==1:
    ans.append(ma[n//2][n//2])
print(max(ans))
```

国王游戏http://cs101.openjudge.cn/practice/28776/

```
n=int(input())
a,b=map(int,input().split())
numbers=[]
for i in range(n):
    ai,bi=map(int,input().split())
    numbers.append((ai,bi))
numbers.sort(key=lambda x:(x[0]*x[1]))
result=0
for i in range(n):
    result=max(result,a//numbers[i][1])
    a*=numbers[i][0]
print(result)
```

孤岛最短距离http://cs101.openjudge.cn/practice/20741/

```
import heapq
n = int(input())
ma = []
for i in range(n):
    ma.append(list(map(int,input())))
m = len(ma[0])
dir = [(-1,0),(1,0),(0,1),(0,-1)]
for i in range(n):
    for j in range(m):
        if ma[i][j]==1:
            x1,y1=i,j
            break
def dij(x1,y1):
    q,visited=[],[[False]*m for _ in range(n)]
    heapq.heappush(q,(0,x1,y1))
    while q:
        step,x,y=heapq.heappop(q)
        if visited[x][y]:
            continue
        visited[x][y] = True
        if ma[x][y]==1 and step!=0:
            return step
        for dx,dy in dir:
            if 0<=x+dx<n and 0<=y+dy<m and not visited[x+dx][y+dy]:
                heapq.heappush(q,(step+1-ma[x+dx][y+dy],x+dx,y+dy))
print(dij(x1,y1))
```

2022双十一http://cs101.openjudge.cn/practice/25561/

```
result = float("inf")
n, m = map(int, input().split())
store_prices = [input().split() for _ in range(n)]
disc = [input().split() for _ in range(m)]
lst = [0] * m

def dfs(i, price):
    global result
    if i == n:
        jian = 0
        for t in range(m):
            st = 0
            for k in disc[t]:
                a, b = map(int, k.split('-'))
                if lst[t] >= a:
                    st = max(st, b)
            jian += st
        result = min(result, price - (price // 300) * 50 - jian)
        return
    
    for u in store_prices[i]:
        idx, p = map(int, u.split(':'))
        lst[idx-1] += p
        dfs(i + 1, price + p)
        lst[idx-1] -= p

dfs(0, 0)
print(result)
```

土豪http://cs101.openjudge.cn/practice/20744/

```
lst = list(map(int, input().split(',')))
dp1 = [0] * len(lst);
dp2 = [0] * len(lst)
dp1[0] = lst[0];
dp2[0] = lst[0]
for i in range(1, len(lst)):
    dp1[i] = max(dp1[i - 1] + lst[i], lst[i])
    dp2[i] = max(dp1[i - 1], dp2[i - 1] + lst[i], lst[i])
print(max(dp2))
```

炸鸡排http://cs101.openjudge.cn/practice/28701/

```
def chic(lst,k):
    if max(lst)<=sum(lst)/k:
        return f'{sum(lst)/k:.3f}'
    else:
        lst.remove(max(lst))
        return chic(lst,k-1)
n,k = map(int,input().split())
lst = list(map(int,input().split()))
print(chic(lst,k))
```

小游戏http://cs101.openjudge.cn/practice/02802/

```
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
        if x1 == y1 == x2 == y2 == 0: break
        s = (x1, y1, -1, 0)
        e = (x2, y2)
        seg = bfs(s, e, board, h, w)
        if seg == -1: print(f"Pair {pair_num}: impossible.")
        else: print(f"Pair {pair_num}: {seg} segments.")
        pair_num += 1
    print()
    board_num += 1
```

水淹七军http://cs101.openjudge.cn/practice/12029/

```
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

跳台阶http://cs101.openjudge.cn/practice/27528/

```
n = int(input())
dp = [0]*(n+1)
dp[0]=1
for i in range(n+1):
    for k in range(i):
        dp[i]+=dp[k]
print(dp[n])
```

马走日http://cs101.openjudge.cn/practice/04123/

```
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

寻宝http://cs101.openjudge.cn/practice/19930/

```
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

田忌赛马http://cs101.openjudge.cn/practice/02287/

```
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

垃圾炸弹http://cs101.openjudge.cn/practice/04133/

```
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

岛屿周长http://cs101.openjudge.cn/practice/12558/

```
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

阿尔法翻译官http://cs101.openjudge.cn/practice/12757/

```
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

充实寒假http://cs101.openjudge.cn/practice/16528/

```
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

零钱兑换http://cs101.openjudge.cn/practice/28780/

```
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

打怪兽http://cs101.openjudge.cn/practice/18182/

```
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

节省存储的矩阵乘法http://cs101.openjudge.cn/practice/23555/

```
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

病人排队http://cs101.openjudge.cn/practice/07618/

```
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

八皇后http://cs101.openjudge.cn/practice/02754/

```
lst = []
def queen(s):
    if len(s)==8:
        lst.append(s)
        return
    for i in range(1,9):
        if all(str(i)!=s[k] and abs(len(s)-k)!=abs(i-int(s[k])) for k in range(len(s))):
            queen(s+str(i))


queen('')
n = int(input())
for i in range(n):
    b = int(input())
    print(lst[b-1])
```

最大最小整数http://cs101.openjudge.cn/practice/12559/

```
n = int(input())
nums = input().split()
for i in range(n - 1):
    for j in range(i+1, n):
        #print(i,j)
        if nums[i] + nums[j] < nums[j] + nums[i]:
            nums[i], nums[j] = nums[j], nums[i]

ans = "".join(nums)
nums.reverse()
print(ans + " " + "".join(nums))
```

排队http://cs101.openjudge.cn/practice/25353/

```
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

罗马数字整数http://cs101.openjudge.cn/practice/28700/

```

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
#字典无序；列表逆序索引写错了
```

ride to schoolhttp://cs101.openjudge.cn/practice/01922/

```
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

黑神话http://cs101.openjudge.cn/20241010mockexam/E28674/

```
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

字符串求和http://cs101.openjudge.cn/20241010mockexam/E28691/

```
lst = input().split()
a, b= int(lst[0][:2]),int(lst[1][:2])
print(a+b)
```

验证身份证号http://cs101.openjudge.cn/20241010mockexam/M28664/

```
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

角谷猜想http://cs101.openjudge.cn/20241010mockexam/M28678/

```
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

机智股民http://cs101.openjudge.cn/20241205mockexam/E22548/

```
lst = list(map(int,input().split()))
a = lst[0]
pro = 0
for i in range(1,len(lst)):
    if lst[i]-a>pro:
        pro = lst[i]-a
    if lst[i]<a:
        a = lst[i]
print(pro)
```

奖学金http://cs101.openjudge.cn/cs1012024feclass11/E28681/

```
n=int(input())
lst=[]
for i in range(1,n+1):
    a,b,c=map(int,input().split())
    s=a+b+c
    lst.append([s,a,-i])
lst.sort(key=lambda x:(x[0],x[1],x[2]),reverse=True)
for j in range(5):
    print(-lst[j][2],lst[j][0])
```

PASCALhttp://cs101.openjudge.cn/cs1012024feclass11/E28908/

```
s=input()
lst=[0,0,0]
for i in range(0,len(s),5):
    if s[i]=='a':
        lst[0]=s[i+3]
    if s[i]=='b':
        lst[1]=s[i+3]
    if s[i]=='c':
        lst[2]=s[i+3]
print(lst[0],lst[1],lst[2])
```

买水果http://cs101.openjudge.cn/cs1012024feclass11/M28699/

```
from collections import defaultdict
a=defaultdict(int)
n,m=map(int,input().split())
lst=list(map(int,input().split()))
lst.sort()
for i in range(m):
    a[input()]+=1
s_a=sorted(a.items(),key=lambda x:x[1],reverse=True)
min_mon=0
max_mon=0
for k in range(len(s_a)):
    min_mon+=s_a[k][1]*lst[k]
    max_mon+=s_a[k][1]*lst[-1-k]
print(min_mon,max_mon)
```

数的划分http://cs101.openjudge.cn/cs1012024feclass11/M28906/

```
n,k=map(int,input().split())
cnt=0
if k==3:
    for i in range(1,n//3+1):
        for j in range(i,n//2+1):
            if n-i-j>=j:
                cnt+=1

if k==4:
    for i in range(1,n//4+1):
        for j in range(i,n//3+1):
            for t in range(j,n//2+1):
                if n-i-j-t>=t:
                    cnt+=1
if k==6:
    for i in range(1,n//6+1):
        for j in range(i,n//5+1):
            for t in range(j,n//4+1):
                for u in range(t,n//3+1):
                    for v in range(u,n//2+1):
                        if n-i-j-t-u-v>=v:
                            cnt+=1
if k==5:
    for j in range(1, n // 5 + 1):
        for t in range(j, n // 4 + 1):
            for u in range(t, n // 3 + 1):
                for v in range(u, n // 2 + 1):
                    if n - j - t - u - v >= v:
                        cnt += 1
if k ==2:
    for i in range(1,n//2+1):
        cnt+=1
print(cnt)
```

温度调节http://cs101.openjudge.cn/cs1012024feclass11/M28914/

```
t=int(input())
for i in range(t):
    cnt=0
    l,r,x=map(int,input().split())
    a,b=map(int,input().split())
    if a==b:
        print(cnt)
        continue
    if (r-b<x and b-l<x) or (r-a<x and a-l<x):
        print(-1)
        continue
    if abs(a-b)>=x:
        print(1)
    elif (a<b and max((a-l),(r-b))>=x) or (a>b and max((r-a),(b-l))>=x):
        print(2)
    else:
        print(3)
```

蛇入迷宫http://cs101.openjudge.cn/practice/28973/

```
import heapq

n = int(input())
maze = [list(map(int, input().split())) for _ in range(n)]

queue = [(0, 0, 0, 0, 1)]
visited = {(0, 0, 0, 1)}

while queue:
    step, tx, ty, hx, hy = heapq.heappop(queue)

    if (tx, ty, hx, hy) == (n - 1, n - 2, n - 1, n - 1):
        print(step)
        break

    if tx == hx:
        if hy + 1 < n and maze[tx][hy + 1] == 0 and (tx, ty + 1, hx, hy + 1) not in visited:
            visited.add((tx, ty + 1, hx, hy + 1))
            heapq.heappush(queue, (step + 1, tx, ty + 1, hx, hy + 1))
        if tx + 1 < n and maze[tx + 1][ty] == 0 and maze[hx + 1][hy] == 0 and (tx + 1, ty, hx + 1, hy) not in visited:
            visited.add((tx + 1, ty, hx + 1, hy))
            heapq.heappush(queue, (step + 1, tx + 1, ty, hx + 1, hy))
        if tx + 1 < n and maze[tx + 1][ty] == 0 and maze[tx + 1][hy] == 0 and (tx, ty, tx + 1, ty) not in visited:
            visited.add((tx, ty, tx + 1, ty))
            heapq.heappush(queue, (step + 1, tx, ty, tx + 1, ty))

    if ty == hy:
        if hx + 1 < n and maze[hx + 1][ty] == 0 and (tx + 1, ty, hx + 1, hy) not in visited:
            visited.add((tx + 1, ty, hx + 1, hy))
            heapq.heappush(queue, (step + 1, tx + 1, ty, hx + 1, hy))
        if ty + 1 < n and maze[tx][ty + 1] == 0 and maze[hx][hy + 1] == 0 and (tx, ty + 1, hx, hy + 1) not in visited:
            visited.add((tx, ty + 1, hx, hy + 1))
            heapq.heappush(queue, (step + 1, tx, ty + 1, hx, hy + 1))
        if ty + 1 < n and maze[tx][ty + 1] == 0 and maze[hx][hy + 1] == 0 and (tx, ty, tx, ty + 1) not in visited:
            visited.add((tx, ty, tx, ty + 1))
            heapq.heappush(queue, (step + 1, tx, ty, tx, ty + 1))

else:
    print(-1)
#如果在heappop后面入visited会重复访问
```



#### LeetCode

前缀https://leetcode.cn/problems/longest-common-prefix/description/

```
class Solution:
    def longestCommonPrefix(self, strs):
        min_len = min(len(i) for i in strs)
        result = ""
        for i in range(min_len):
            if len(set(s[i]for s in strs)) > 1:
                break
            else:
                result += strs[0][i]
        return result   
```

有效括号https://leetcode.cn/problems/valid-parentheses/description/

```
class Solution:
    def isValid(self, s: str) -> bool:
        dic = {")":"(", "]":"[", "}":"{"}
        stack = []
        for i in s:
            if stack and i in dic:
                if stack[-1] == dic[i]:
                    stack.pop()
                else:
                    return False
            else:
                stack.append(i)
                
        return not stack    
```

https://leetcode.cn/problems/remove-duplicates-from-sorted-array/description/

```
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        k = 1 
        for i in range(1, len(nums)):
            if nums[i] != nums[i-1]:
                nums[k] = nums[i]
                k += 1
        return k 
```

https://leetcode.cn/problems/remove-element/description/

```
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        k = 0
        for i in range(len(nums)):
            if nums[i] != val:
                nums[k] = nums[i]
                k += 1
        return k
```

https://leetcode.cn/problems/find-the-index-of-the-first-occurrence-in-a-string/description/

```
class Solution:
    def strStr(self, haystack: str, needle: str) -> int:
        if needle not in haystack:
            return -1
        else:
            for i in range(len(haystack)):
                if haystack[i:len(needle)+i] == needle[:]:
                    return i
```

https://leetcode.cn/problems/merge-two-sorted-lists/description/

```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def mergeTwoLists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:
        if list1 == None:
            return list2
        if list2 == None:
            return list1
        if list1.val <= list2.val:
            list1.next = self.mergeTwoLists(list1.next, list2)
            return list1
        else:
            list2.next = self.mergeTwoLists(list1, list2.next)
            return list2
```

https://leetcode.cn/problems/length-of-last-word/description/

```
class Solution:
    def lengthOfLastWord(self, s: str) -> int:
        i = len(s) - 1
        while s[i] == " ":
            i -= 1
        j = i - 1
        while j >= 0 and s[j] != " ":
            j -= 1
        return i - j
```

https://leetcode.cn/problems/plus-one/description/

```
class Solution:
    def plusOne(self, digits: List[int]) -> List[int]:
        for i in range(len(digits)-1, -1, -1):
            if digits[i] != 9:
                digits[i] += 1
                return digits
            else:
                digits[i] = 0
                if digits[0] == 0:
                    digits.insert(0, 1)
                    return digits
```

https://leetcode.cn/problems/unique-paths/description/

```
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        ans = 1
        for i in range(m,m+n-1):
            ans *=i
        for k in range(1,n):
            ans //= k
        return ans
```

https://leetcode.cn/problems/add-binary/description/

```
class Solution:
    def addBinary(self, a: str, b: str) -> str:
        alist = list(a)
        blist = list(b)
        at = 0
        bt = 0
        for i in range(len(alist)):
            at += 2**i*int(alist[-i-1])
        for j in range(len(blist)):
            bt += 2**j*int(blist[-j-1])
        sum = at + bt
        result = bin(sum)[2:]
        return result
```

https://leetcode.cn/problems/sqrtx/description/

```
class Solution:
    def mySqrt(self, x: int) -> int:
        for i in range(0, x+1):
            if i*i <= x < (i+1)*(i+1):
                return i

```



##### 双指针：

https://leetcode.cn/problems/3sum/description/

```
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        nums=sorted(nums)
        n=len(nums)
        res=[]
        for first in range(n):
            if first > 0 and nums[first] == nums[first - 1]:
                continue
            third = n - 1
            target = -nums[first]
            for second in range(first + 1, n):
                if second > first + 1 and nums[second] == nums[second - 1]:
                    continue
                while second < third and nums[second] + nums[third] > target:
                    third -= 1
                if second == third:
                    break
                if nums[second] + nums[third] == target:
                    res.append([nums[first], nums[second], nums[third]])
        return res
#第二重循环和第三重循环实际上是并列的关系
```

https://leetcode.cn/problems/container-with-most-water/description/

```
class Solution:
    def maxArea(self, height: List[int]) -> int:
        n=len(height)
        s=0
        e=n-1
        res=min(height[s],height[e])*(e-s)
        while s<e:
            if height[s]<height[e]:
                s+=1
                res=max(res,min(height[s],height[e])*(e-s))
            else:
                e-=1
                res=max(res,min(height[s],height[e])*(e-s))
        return res
```

https://leetcode.cn/problems/trapping-rain-water/description/

```
class Solution:
    def trap(self, height: List[int]) -> int:
       
        stack = []
        water = 0
        for i in range(len(height)):
            while stack and height[i] > height[stack[-1]]:
                top = stack.pop()
                if not stack:
                    break
                distance = i - stack[-1] - 1
                bounded_height = min(height[i], height[stack[-1]]) - height[top]
                water += distance * bounded_height
            stack.append(i)
        return water 
```



##### 矩阵：

https://leetcode.cn/problems/rotate-image/solutions/526980/

```
class Solution:
    def rotate(self, matrix: List[List[int]]) -> None:
        n = len(matrix)
        matrix_new = [[0] * n for _ in range(n)]
        for i in range(n):
            for j in range(n):
                matrix_new[j][n - i - 1] = matrix[i][j]
        matrix[:] = matrix_new
        # 不能写成 matrix = matrix_new
        # matrix = matrix_new
#这只是将变量 matrix 重新绑定到新的对象 matrix_new，但这不会修改原始列表的内容。函数外部仍然引用的是传
#入的旧对象，因此从外部观察，传入的 matrix 并没有任何改变。
#matrix[:] = matrix_new
#这一写法是对 matrix 的内容进行原地修改（in-place operation）。它并不会改变 matrix 的引用，而是将 #matrix_new 的内容复制到 matrix 中，从而保证原始列表对象被更新
```

```
class Solution:
    def rotate(self, matrix: List[List[int]]) -> None:
        n = len(matrix)
        for i in range(n // 2):
            for j in range((n + 1) // 2):
                matrix[i][j], matrix[n - j - 1][i], matrix[n - i - 1][n - j - 1], matrix[j][n - i - 1] \
                    = matrix[n - j - 1][i], matrix[n - i - 1][n - j - 1], matrix[j][n - i - 1], matrix[i][j]
```

  https://leetcode.cn/problems/search-a-2d-matrix-ii/description/

```
class Solution:
    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
        for row in matrix:
            i = bisect.bisect_left(row, target)
            if i < len(row) and row[i] == target:
                return True
        return False
```

https://leetcode.cn/problems/spiral-matrix/

```
from ast import literal_eval
from typing import List
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



##### 贪心：

https://leetcode.cn/problems/jump-game/description/

```
class Solution:
    def canJump(self, nums: List[int]) -> bool:
        n, m = len(nums), 0
        for i in range(n):
            if i <= m:
                m = max(m, i + nums[i])
                if m >= n - 1:
                    return True
        return False
```

https://leetcode.cn/problems/jump-game-ii/description/

```
class Solution:
    def jump(self, nums: List[int]) -> int:
        p = len(nums) - 1
        step = 0
        while p > 0:
            for i in range(p):
                if i + nums[i] >= p:
                    p = i
                    step += 1
                    break
        return step
```

https://leetcode.cn/problems/partition-labels/description/

```
class Solution:
    def partitionLabels(self, s: str) -> List[int]:
        lt = [0] * 26
        for i, l in enumerate(s):
            lt[ord(l) - ord("a")] = i        
        lst=[]
        start = end = 0
        for i, l in enumerate(s):
            end = max(end, lt[ord(l) - ord("a")])
            if i == end:
                lst.append(end - start + 1)
                start = end + 1        
        return lst
```



##### dp：

https://leetcode.cn/problems/wiggle-subsequence/description/

```
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

https://leetcode.cn/problems/longest-palindromic-substring/

```
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

https://leetcode.cn/problems/word-break/description/

```
class Solution:
    def wordBreak(self, s: str, wordDict: List[str]) -> bool:       
        n=len(s)
        dp=[False]*(n+1)
        dp[0]=True
        for i in range(n):
            for j in range(i+1,n+1):
                if(dp[i] and (s[i:j] in wordDict)):
                    dp[j]=True
        return dp[-1]
```

https://leetcode.cn/problems/longest-valid-parentheses/

```
class Solution:
    def longestValidParentheses(self, s: str) -> int:
        max_ans = 0  
        n = len(s)  
        dp = [0] * n            
        for i in range(1, n):  
            if s[i] == ')':  
                if s[i - 1] == '(':  
                    dp[i] = (dp[i - 2] if i >= 2 else 0) + 2  
                elif i - dp[i - 1] > 0 and s[i - dp[i - 1] - 1] == '(':  
                    dp[i] = dp[i - 1] + (dp[i - dp[i - 1] - 2] if i - dp[i - 1] >= 2 else 0) + 2  
                max_ans = max(max_ans, dp[i])            
        return max_ans
```

https://leetcode.cn/problems/edit-distance/description/

```
class Solution:
    def minDistance(self, word1: str, word2: str) -> int:
        n = len(word1)
        m = len(word2)
        if n * m == 0:
            return n + m
        dp = [ [0] * (m + 1) for _ in range(n + 1)]
        for i in range(n + 1):
            dp[i][0] = i
        for j in range(m + 1):
            dp[0][j] = j
        for i in range(1, n + 1):
            for j in range(1, m + 1):
                a = dp[i - 1][j] + 1
                b = dp[i][j - 1] + 1
                c = dp[i - 1][j - 1] 
                if word1[i - 1] != word2[j - 1]:
                    c += 1
                dp[i][j] = min(a, b, c)
        return dp[n][m]
```

