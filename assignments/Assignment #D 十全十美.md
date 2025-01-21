# Assignment #D: 十全十美 

Updated 1254 GMT+8 Dec 17, 2024

2024 fall, Complied by <mark>王梓航、物理学院</mark>



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 02692: 假币问题

brute force, http://cs101.openjudge.cn/practice/02692

思路：假币在不平衡的情况下应该归属于同一边，且其不属于平衡结果中的部分，所以用集和处理



代码：

```python
n = int(input())
for _ in range(n):
    d,e,f=set('ABCDEFGHIJKL'),set('ABCDEFGHIJKL'),set()
    for j in range(3):
        a,b,c=input().split()
        if c=='even':
            f=f|set(a+b)
        elif c=='up':
            d= d&set(a)
            e = e&set(b)
        else:
            d = d&set(b)
            e = e&set(a)
    g = d&f
    h = e&f
    e-=h
    d-=g
    if d:
        s = list(d)[0]
        print('{} is the counterfeit coin and it is heavy.'.format(s))
        continue
    s = list(e)[0]
    print('{} is the counterfeit coin and it is light.'.format(s))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![ad657f960d12e37283ebe57581c69cd](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\ad657f960d12e37283ebe57581c69cd.png)



### 01088: 滑雪

dp, dfs similar, http://cs101.openjudge.cn/practice/01088

思路：正常从每一个局域最大值往下找即可。做起来感觉和水淹七军有些类似



代码：

```python
import heapq
from collections import deque
r,c=map(int,input().split())
a = [list(map(int,input().split())) for _ in range(r)]
dir=[(-1,0),(1,0),(0,1),(0,-1)]
visited=[[0]*c for _ in range(r)]
result=0
for i in range(r):
    for j in range(c):
        if visited[i][j]!=0:
            continue
        for dx,dy in dir:
            pi,pj=i+dx,j+dy
            if 0<=pi<r and 0<=pj<c and a[pi][pj]>a[i][j]:
                break
        else:
            visited[i][j]=1
            queue=[]
            heapq.heappush(queue,(-a[i][j],i,j,1))
            while queue:
                h,x,y,count=heapq.heappop(queue)
                if visited[x][y]!=count:
                    continue
                for dx,dy in dir:
                    px,py=x+dx,y+dy
                    if 0<=px<r and 0<=py<c and a[px][py]<-h and visited[px][py]<count+1:
                        visited[px][py]=count+1
                        heapq.heappush(queue,(-a[px][py],px,py,count+1))
print(max([max(index) for index in visited]))
```



代码运行截图 ==（至少包含有"Accepted"）==

![630bf443cbdfad38659e5f399654f6c](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\630bf443cbdfad38659e5f399654f6c.png)



### 25572: 螃蟹采蘑菇

bfs, dfs, http://cs101.openjudge.cn/practice/25572/

思路：正常bfs搜索即可，只有微小差别。



代码：

```python
import heapq
dir=[(1,0),(-1,0),(0,1),(0,-1)]
n = int(input())
a = [list(map(int,input().split())) for _ in range(n)]
for i in range(n):
    for j in range(n):
        if a[i][j]==5:
            x1,y1=i,j
            if j+1<n and a[i][j+1]==5:
                x2,y2=i,j+1
            if i+1<n and a[i+1][j]==5:
                x2,y2=i+1,j
            visited=[[False]*n for _ in range(n)]
            queue=[]
            heapq.heappush(queue,[0,x1,y1,x2,y2])
            visited[x1][y1]=True
            while queue:
                count,p1,q1,p2,q2=heapq.heappop(queue)
                if a[p1][q1]==9 or a[p2][q2]==9:
                    print('yes')
                    break
                for dx,dy in dir:
                    px1,py1,px2,py2=p1+dx,q1+dy,p2+dx,q2+dy
                    if 0<=px1<n and 0<=py1<n and 0<=px2<n and 0<=py2<n and a[px1][py1]!=1 and a[px2][py2]!=1 and not visited[px1][py1]:
                        visited[px1][py1]=True
                        heapq.heappush(queue,[count+1,px1,py1,px2,py2])
            else:
                print('no')
            exit(0)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![dd5732ba7bf463e4556eb4fc4b9dfff](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\dd5732ba7bf463e4556eb4fc4b9dfff.png)



### 27373: 最大整数

dp, http://cs101.openjudge.cn/practice/27373/

思路：和之前排序的题类似，但是最后要dp处理一下



代码：

```python
import functools
def key1(a,b):
    if int(a+b)>int(b+a):
        return 1
    elif int(a+b)==int(b+a):
        return 0
    else:
        return -1
key2=functools.cmp_to_key(key1)
n = int(input())
m = int(input())
a = input().split()
a.sort(key=key2,reverse=True)
dp=['']*(n+1)
for index in a:
   l=len(index)
   for t in range(n-l,0,-1):
       if dp[t]!='':
           dp[t+l]=max(dp[t+l],dp[t]+index)
   if dp[l]=='':
       dp[l]=index
for index in dp[::-1]:
    if index!='':
        print(int(index))
        break
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![93b7bcc996ddda2bd3f483727248cd7](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\93b7bcc996ddda2bd3f483727248cd7.png)



### 02811: 熄灯问题

brute force, http://cs101.openjudge.cn/practice/02811

思路：只用看一列的情况即可，强行枚举即可。



代码：

```python
g={}
for i in range(5):
    g[(i,-1)]=0
    g[(i,6)]=0
for j in range(-1,7):
    g[(-1,j)]=0
    g[(5,j)]=0
f=[[],[],[],[],[]]
for i in range(5):
    f[i]=list(map(int,input().split()))
for s in range(32):
    a=s
    for i in range(5):
        g[(i,0)]=a%2
        a=a//2
    for j in range(1,6):
        for i in range(5):
            g[(i,j)]=(f[i][j-1]+g[(i,j-1)]+g[(i-1,j-1)]+g[(i+1,j-1)]+g[(i,j-2)])%2
    x=0
    for i in range(5):
        x+=(f[i][5]+g[(i,5)]+g[(i-1,5)]+g[(i+1,5)]+g[(i,4)])%2
    if x==0 :
        for i in range(5):
            print(*[g[i,j] for j in range(6)])
        break
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![e98a52ce7c1649321050f030c78de83](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\e98a52ce7c1649321050f030c78de83.png)



### 08210: 河中跳房子

binary search, greedy, http://cs101.openjudge.cn/practice/08210/

思路：二分查找，做过aggressive cow，所以就是一样处理



代码：

```python
l,n,m=map(int,input().split())
b = [int(input()) for _ in range(n)]
right = l//(n-m+1)
left = 0
if n==m:
    print(l)
    exit()
def can_reach(d):
    a = 0
    count=0
    for index in b:
        if index-a>=d:
            count+=1
            a = index
        if count==n-m:
            return l-index>=d
    return False
result=0
while left <= right:
    mid = (right+left)//2
    if can_reach(mid):
        result=mid
        left=mid+1
    else:
        right = mid-1
else:
    print(result)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![133dc7da0b90073a525f4792b7fa58b](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\133dc7da0b90073a525f4792b7fa58b.png)



## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>

每日选做做完了。做了前两年卷子，基本有个底了。这周计划看看做过的题，看看答案，准备下cheating sheet。