# Assignment #4: T-primes + 贪心

Updated 0337 GMT+8 Oct 15, 2024

2024 fall, Complied by <mark>王梓航，物理学院</mark>



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 34B. Sale

greedy, sorting, 900, https://codeforces.com/problemset/problem/34/B



思路：排序找就好了（之前写的代码，有点冗杂）



代码

```python
# a=input().split()
b=input().split()
c=int(a[0])
d=int(a[1])
for i in range(c):
    b[i]=int(b[i])
b.sort()
j=0
 
x=0
for i in b:
    if j<d and i<0:
        x+=-i
        j+=1
    if j==d:
        break
 
print(x)

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![4949c7e7761903305649e3e1c9a8ff0](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\4949c7e7761903305649e3e1c9a8ff0.png)



### 160A. Twins

greedy, sortings, 900, https://codeforces.com/problemset/problem/160/A

思路：



代码

```python
a=int(input())
b=input().split()
for i in range(a):
    b[i]=int(b[i])
b.sort(reverse=True)
i=0
def sum(a,b):
    m=0
    for i in range(b):
        m=m+a[i]
    return m
while(2*sum(b,i)<=sum(b,a)):
    if i==b:
        break
    i=i+1
      
print(i)

```



代码运行截图 ==（至少包含有"Accepted"）==

![840ae0f516a945600f1c4ebc70a515f](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\840ae0f516a945600f1c4ebc70a515f.png)



### 1879B. Chips on the Board

constructive algorithms, greedy, 900, https://codeforces.com/problemset/problem/1879/B

思路：



代码

```python
N=int(input())
x=[]
for i in range(N):
    a=int(input())
    m_i=input().split()
    n_i=input().split()
    for j in range(a):
        m_i[j]=int(m_i[j])
        n_i[j]=int(n_i[j])
    summ_i=0
    sumn_i=0
    for k in range(a):
        summ_i=summ_i+m_i[k]
        sumn_i=sumn_i+n_i[k]
    x.append(min(min(m_i)*a+sumn_i,min(n_i)*a+summ_i))
 
for i in range(N):
    print(x[i])

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![e0da1062ffbc1677c4bd39992179287](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\e0da1062ffbc1677c4bd39992179287.png)



### 158B. Taxi

*special problem, greedy, implementation, 1100, https://codeforces.com/problemset/problem/158/B

思路：



代码

```python
import math
from collections import Counter
input()
a = Counter(map(int,input().split()))
n = a[4]+a[3]+math.ceil(a[2]/2)
if a[1]>a[3]+2*int(a[2]%2==1):
    print()
    n+=math.ceil((a[1]-a[3]-2*int(a[2]%2==1))/4)
print(n

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![14d62977d4446e4409972c74c718ab5](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\14d62977d4446e4409972c74c718ab5.png)



### *230B. T-primes（选做）

binary search, implementation, math, number theory, 1300, http://codeforces.com/problemset/problem/230/B

思路：

先得到质数表再处理，当然很多的细节是看了同学的做法学习的

代码

```python
import array
 
N = int(input())
a = array.array('q',map(int,input().split()))
f = [True]*(10**6)
g = []
for i in range(2,5*10**5):
    if f[i-1]:
        g.append(i)
    for index in g:
        if i*index>10**6-1:
            break
        f[i*index-1]=False
        if i%index==0:
            break
h = set(index**2 for index in range(2,10**6) if f[index-1])
print('\n'.join(['YES' if index in h else 'NO' for index in a]))

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![d5c4d60b0abf1af4f3cf24c0c564765](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\d5c4d60b0abf1af4f3cf24c0c564765.png)



### *12559: 最大最小整数 （选做）

greedy, strings, sortings, http://cs101.openjudge.cn/practice/12559

思路：用前后排列比较两个数，用cmp_to_key处理排序



代码

```python
from functools import cmp_to_key
def compare(x,y):
    if int(x+y)<int(y+x):
        return -1
    elif int(y+x)>int(x+y):
        return 1
    else:
        return 0
key_func=cmp_to_key(compare)
input()
a = input().split()
a.sort(key=key_func,reverse=True)
print(''.join(a), end = ' ')
print(''.join(a[::-1]))

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![858903aed59599eef4358f8d144cc3f](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\858903aed59599eef4358f8d144cc3f.png)



## 2. 学习总结和收获

每日选做一直在跟进。

很多题目都感觉很有意思，像是最后一题，因为一开始我是做的洛谷上的这题，没有提示，确实做着做着才想到这么比较，自己废了老大力气写插入排序，优化成归并排序，结果问通义发现有内置函数直接处理。感觉自己要学的还很多。

