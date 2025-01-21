# Assignment #6: Recursion and DP

Updated 2201 GMT+8 Oct 29, 2024

2024 fall, Complied by <mark>王梓航，物理学院</mark>



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### sy119: 汉诺塔

recursion, https://sunnywhy.com/sfbj/4/3/119  

思路：递推地写即可



代码：

```python
def get(n,a,b,c):
  A = format(a)
  B = format(b)
  C = format(c)
  if n==1:
    print(f'{A}->{C}')
    return
  get(n-1,a,c,b)
  print(f'{A}->{c}')
  get(n-1,b,a,c)
n = int(input())
print(2**n-1)
get(n,'A','B','C')

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![fabd88ec48e66a169c3ad42713d35bd](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\fabd88ec48e66a169c3ad42713d35bd.png)



### sy132: 全排列I

recursion, https://sunnywhy.com/sfbj/4/3/132

思路：用内置函数处理的



代码：

```python
n = int(input())
from itertools import permutations
a = permutations(list(range(1,n+1)))
for index in a:
    print(*index)
```



代码运行截图 ==（至少包含有"Accepted"）==

![f46879f44f652651b7e1e53a39d3569](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\f46879f44f652651b7e1e53a39d3569.png)



### 02945: 拦截导弹 

dp, http://cs101.openjudge.cn/2024fallroutine/02945

思路：递推地处理



代码：

```python
n = int(input())
a = list(map(int,input().split()))
f=[(1,a[0])]
for i in range(1,n):
    g = [(1, a[i])]
    for j in range(i):
        if f[j][1]>=a[i]:
            g.append((f[j][0]+1,a[i]))
    g.sort()
    f.append(g[-1])
f.sort()
print(f[-1][0])
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![da1d2926b31d447c08ed257e5645202](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\da1d2926b31d447c08ed257e5645202.png)



### 23421: 小偷背包 

dp, http://cs101.openjudge.cn/practice/23421

思路：双数列递推处理



代码：

```python
n,m=map(int,input().split())
f=[[0,0]]
a = list(map(int,input().split()))
b = list(map(int,input().split()))
c = list(zip(a,b))
for i,j in c:
    g=[]
    for index in f:
        if index[1]+j<=m:
            g.append([index[0]+i,index[1]+j])
    f+=g
print(max([index[0] for index in f]))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>



![513d68f10e6d01c26b2593ffb9a29fc](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\513d68f10e6d01c26b2593ffb9a29fc.png)

### 02754: 八皇后

dfs and similar, http://cs101.openjudge.cn/practice/02754

思路：基本思路和主流的差不多，但是当时使用一个二维表格实现的，比较麻烦。



代码：

```python
n = int(input())
a = [int(input()) for _ in range(n)]
g = []
b = [[True] * 8 for _ in range(8)]

def f(i, result, b_copy):
    for j in range(8):
        if b_copy[i][j]:
            if i == 7:
                g.append(result + [str(j+1)])
                return
            b_next = [row[:] for row in b_copy]  
            for t in range(i + 1, 8):
                b_next[t][j] = False
                if t - i + j <= 7:
                    b_next[t][t - i + j] = False
                if j-t+i>=0:
                    b_next[t][j-t+i]=False
            f(i + 1, result + [str(j+1)], b_next)

f(0, [], b)
print('\n'.join([''.join(g[i-1]) for i in a]))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241031213134457](C:\Users\王\AppData\Roaming\Typora\typora-user-images\image-20241031213134457.png)



### 189A. Cut Ribbon 

brute force, dp 1300 https://codeforces.com/problemset/problem/189/A

思路：递推地处理



代码：

```python
n,a,b,c=map(int,input().split())
f = {a,b,c}
g = []
for index in f:
    if index <=n:
        g.append(index)
f=sorted(g)
dp=[-1]*(n+1)
for index in f:
    dp[index]=1
for i in range(f[0],n+1):
    for j in f:
        if i-j>=1 and dp[i-j]!=-1:
            dp[i]=max(dp[i],dp[i-j]+1)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![e2dccae8ea5dc57b504e8246bddbc13](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\e2dccae8ea5dc57b504e8246bddbc13.png)



## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>

最近准备期中，每日选做只做了一部分，期中过后还是打算补回来。