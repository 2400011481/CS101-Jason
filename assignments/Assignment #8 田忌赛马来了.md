# Assignment #8: 田忌赛马来了

Updated 1021 GMT+8 Nov 12, 2024

2024 fall, Complied by <mark>王梓航，物理学院</mark>



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 12558: 岛屿周⻓

matices, http://cs101.openjudge.cn/practice/12558/ 

思路：正常多加一圈就可以了



代码：

```python
n,m = map(int,input().split())
g = [(-1,0),(1,0),(0,1),(0,-1)]
s = 0
f = [[0]*(m+2)]+[[0]+list(map(int,input().split()))+[0] for _ in range(n)]+[[0]*(m+2)]
for i in range(1,n+1):
    for j in range(1,m+1):
        if f[i][j]==1:
         for p,q in g:
            if f[i+p][j+q]==0:
                s+=1
print(s)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![e17927dff6fe180fe032d99e4cef322](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\e17927dff6fe180fe032d99e4cef322.png)



### LeetCode54.螺旋矩阵

matrice, https://leetcode.cn/problems/spiral-matrix/

与OJ这个题目一样的 18106: 螺旋矩阵，http://cs101.openjudge.cn/practice/18106

思路：递归地处理



代码：

```python
def get(n):
    if n==1:
        return [[1]]
    a = get(n-1)
    f = [[0]*n for _ in range(n)]
    for index in range(n):
        f[0][index]=index+1
    for index in range(n,2*n-1):
        f[index-n+1][n-1]=index+1
    for i in range(1,n):
        for j in range(n-1):
            f[i][j]=a[n-1-i][n-2-j]+2*n-1
    return f
n = int(input())
a = get(n)
for index in a:
    print(*index)
```



代码运行截图 ==（至少包含有"Accepted"）==

![2a49e9dd6af5d6d781bee6737d52b82](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\2a49e9dd6af5d6d781bee6737d52b82.png)



### 04133:垃圾炸弹

matrices, http://cs101.openjudge.cn/practice/04133/

思路：在周围一圈查找



代码：

```python
d = int(input())
n = int(input())
c = {}
for i in range(n):
    x,y,z=map(int,input().split())
    for p in range(max(0,x-d),min(1024,x+d)+1):
        for q in range(max(0,y-d),min(1024,y+d)+1):
            c[(p,q)]=c.setdefault((p,q),0)+z
a = list(c.values())
s = max(a)
print(a.count(s),s)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![cf2119daa52d7811a85636aeefa92eb](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\cf2119daa52d7811a85636aeefa92eb.png)



### LeetCode376.摆动序列

greedy, dp, https://leetcode.cn/problems/wiggle-subsequence/

与OJ这个题目一样的，26976:摆动序列, http://cs101.openjudge.cn/routine/26976/

思路：构造一个最长摆动序列，类似的处理



代码：

```python
n = int(input())
a = list(map(int,input().split()))
r = [a[0]]
for i in range(1,n):
    if len(r)==1 and a[i]!=a[0]:
        r.append(a[i])
    elif a[i]<r[-1]>r[-2] or a[i]>r[-1]<r[-2]:
        r.append(a[i])
    else:
        r.pop()
        r.append(a[i])
print(len(r))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![b31aac57d2f436d8a1edf6644f8bd0c](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\b31aac57d2f436d8a1edf6644f8bd0c.png)



### CF455A: Boredom

dp, 1500, https://codeforces.com/contest/455/problem/A

思路：正常递推即可



代码：

```python
from collections import Counter
input()
a = Counter(map(int,input().split()))
b = sorted(a.keys())
n = len(b)
if n==1:
    print(b[0]*a[b[0]])
else:
    dp=[0]*n
    dp[0]=a[b[0]]*b[0]
    dp[1]=max(a[b[0]]*b[0]+int((b[1]-b[0])>1)*a[b[1]]*b[1],a[b[1]]*b[1])
    for i in range(2,n):
        dp[i]=max(dp[i-1]+int((b[i]-b[i-1])>1)*a[b[i]]*b[i],dp[i-2]+a[b[i]]*b[i])
    print(dp[-1])
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![87c10039ff80ecd1784381a3e5e9388](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\87c10039ff80ecd1784381a3e5e9388.png)



### 02287: Tian Ji -- The Horse Racing

greedy, dfs http://cs101.openjudge.cn/practice/02287

思路：看了答案才想清楚，遇到相等的情况可以先等等，处理完了再分析。思路确实很巧妙。



代码：

```python
from collections import deque
while True:
    n = int(input())
    if n == 0:
        break
    a = deque(sorted(list(map(int,input().split()))))
    b = deque(sorted(list(map(int,input().split()))))
    s=0
    while a:
        if a[-1]>b[-1]:
            s+=1
            a.pop()
            b.pop()
        elif a[0]>b[0]:
            s+=1
            a.popleft()
            b.popleft()
        else:
            if a[0]<b[-1]:
                s-=1
            a.popleft()
            b.pop()
    print(s*200)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![7719456e8794279207158eff0c4d514](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\7719456e8794279207158eff0c4d514.png)



## 2. 学习总结和收获

感觉题目有点跟不上了，接下来要多花些时间。