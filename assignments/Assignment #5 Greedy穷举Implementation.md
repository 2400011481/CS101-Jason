# Assignment #5: Greedy穷举Implementation

Updated 1939 GMT+8 Oct 21, 2024

2024 fall, Complied by <mark>王梓航，物理学院</mark>



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 04148: 生理周期

brute force, http://cs101.openjudge.cn/practice/04148

思路：枚举处理



代码：

```python
x=0
while True:
    x+=1
    a=list(map(int,input().split()))
    if a==[-1,-1,-1,-1]:
        break
    j=1
    while True:
        if (a[0]+j*23-a[1])%28==0 and (a[0]+j*23-a[2])%33==0:
            print('Case {}: the next triple peak occurs in {} days.'.format(x,a[0]+j*23-a[3]))
            break
        else: j+=1
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![87060f80f8a70e60016064b20d65e28](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\87060f80f8a70e60016064b20d65e28.png)



### 18211: 军备竞赛

greedy, two pointers, http://cs101.openjudge.cn/practice/18211

思路：先处理能处理的，再前后一对对地处理，注意判断是否值得卖武器



代码：

```python
a = int(input())
from collections import deque
b = list(map(int,input().split()))
b.sort()
b=deque(b)
flag=False
n=0
for index in b:
    if index<=a:
        flag=True
        a+=-index
        n+=1
    else:
        break
for _ in range(n):
    b.popleft()

while a<sum(list(b)[0:-1]) and flag:
    a+=b[-1]-b[0]
    b.pop()
    b.popleft()
if flag:
    for index in b:
        if index <= a:
            a += -index
            n += 1
        else:
            break
    print(n)
else:
    print(0)
```



代码运行截图 ==（至少包含有"Accepted"）==

![ee87724b0ca1662244a6b630fd7dd0c](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\ee87724b0ca1662244a6b630fd7dd0c.png)



### 21554: 排队做实验

greedy, http://cs101.openjudge.cn/practice/21554

思路：用时越少的排的越前。



代码：

```python
n = int(input())
f = list(map(int,input().split()))
g = [(f[i],i) for i in range(n)]
g.sort()
a = sum([g[i][0]*(n-i-1) for i in range(n)])/n
b = format(a,'.2f')
print(' '.join([str(index[1]+1) for index in g]))
print(f'{b}')
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![06593b59246d0357a2c4633b3851fc7](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\06593b59246d0357a2c4633b3851fc7.png)



### 01008: Maya Calendar

implementation, http://cs101.openjudge.cn/practice/01008/

思路：按照输入转换即可。注意到日是从零开始计算的，所以直接用题目的数据就不会出现一年的最后一天要特殊判断。



代码：

```python
e = ['pop', 'no', 'zip', 'zotz', 'tzec', 'xul', 'yoxkin', 'mol', 'chen', 'yax', 'zac', 'ceh', 'mac', 'kankin', 'muan', 'pax', 'koyab', 'cumhu','uayet']
f = ['imix', 'ik', 'akbal', 'kan', 'chicchan', 'cimi', 'manik', 'lamat', 'muluk', 'ok', 'chuen', 'eb', 'ben', 'ix', 'mem', 'cib', 'caban', 'eznab', 'canac', 'ahau']
dic_month={}
j=0
for i,index in enumerate(e):
    dic_month[index]=i*20
def translate(a,b,c):
    n=c*365+int(dic_month[b])+a
    y=n//260
    days=n%260
    num_month=(days)%13+1
    num_day=days%20
    print(num_month,f[num_day],y)
n = int(input())
print(n)
for _ in range(n):
    a,b,c=input().split()
    a = int(a[:-1])
    c = int(c)
    translate(a,b,c)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![cc19a1d7324ef6eab35359e430a6eed](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\cc19a1d7324ef6eab35359e430a6eed.png)



### 545C. Woodcutters

dp, greedy, 1500, https://codeforces.com/problemset/problem/545/C

思路：找到所有可以倒下的区间，然后类似区间覆盖处理。



代码：

```python
n = int(input())
f = [list(map(int,input().split())) for _ in range(n)]
g=[]
for i in range(n):
    if i==0 or f[i-1][0]<f[i][0]-f[i][1]:
        g.append((f[i][0]-f[i][1],f[i][0]))
    if i==n-1 or f[i][0]+f[i][1]<f[i+int(i!=n-1)][0]:
        g.append((f[i][0],f[i][0]+f[i][1]))
ma=g[-1][0]
sum=1
for index in g[-1::-1]:
    if index[1]<ma:
        sum+=1
        ma=index[0]
print(sum)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![a9412b666b8297cb469767b97d178a3](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\a9412b666b8297cb469767b97d178a3.png)



### 01328: Radar Installation

greedy, http://cs101.openjudge.cn/practice/01328/

思路：和进程检测类似处理即可



代码：

```python
import math
m=0
while True:
    m+=1
    a,b=map(int,input().split())
    if a==0 and b==0:
        break
    f=[]
    flag=True
    for i in range(a):
        x,y=map(int,input().split())
        if y<=b:
          r = math.sqrt(b**2-y**2)
          f.append((x-r,x+r))
        else:
            flag=False
    if flag:
      f.sort()
      n=1
      j=f[-1][0]
      for i in f[::-1]:
          if i[1]>=j:
              continue
          else:
              j=i[0]
              n+=1
    else:
      n=-1
    print('Case {}: {}'.format(m,n))
    input(
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![c745777c1d96ce65ff6891d24024cf9](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\c745777c1d96ce65ff6891d24024cf9.png)



## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>

每日选做一直在跟进，也有做晴问的部分题。最近做题找思路的时间一般都很长，感觉还需要多做题找感觉。