# Assignment #9: dfs, bfs, & dp

Updated 2107 GMT+8 Nov 19, 2024

2024 fall, Complied by <mark>王梓航，物理学院</mark>



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 18160: 最大连通域面积

dfs similar, http://cs101.openjudge.cn/practice/18160

思路：dfs处理即可



代码：

```python
import sys
sys.setrecursionlimit(20000)
m = int(input())
def dfs(x,y,count):
    count+=1
    a[x][y]='.'
    for p,q in [(-1,1),(-1,0),(-1,-1),(0,1),(0,-1),(1,1),(1,0),(1,-1)]:
        x1=x+p
        y1=y+q
        if 0<=x1<=s-1 and 0<=y1<=t-1:
            if a[x1][y1]=='W':
                count = dfs(x1,y1,count)
    return count
for _ in range(m):
    s,t=map(int,input().split())
    a = [list(input()) for index in range(s)]
    sum1=0
    for i in range(s):
        for j in range(t):
            if a[i][j]=='W':
                d = dfs(i,j,0)
                sum1=max(sum1,d)
    print(sum1)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![d8eac79be2fa525b86f9b734ade211a](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\d8eac79be2fa525b86f9b734ade211a.png)



### 19930: 寻宝

bfs, http://cs101.openjudge.cn/practice/19930

思路：用heapq处理，参考了答案的做法，感觉这样确实很方便



代码：

```python
import heapq
i, j = map(int, input().split())
a = [list(map(int, input().split())) for _ in range(i)]
queue = []
vis = [[False] * j for _ in range(i)]
dir = [(0, 1), (0, -1), (1, 0), (-1, 0)]
heapq.heappush(queue, (0, 0, 0))
vis[0][0] = True
while queue:
    step, x, y = heapq.heappop(queue)
    if a[x][y] == 1:
        print(step)
        exit(0)
    for (dx, dy) in dir:
        px, py = x + dx, y + dy
        if 0 <= px < i and 0 <= py < j and not vis[px][py] and a[px][py] != 2:
            vis[px][py] = True
            heapq.heappush(queue, (step + 1, px, py))
print('NO')
```



代码运行截图 ==（至少包含有"Accepted"）==

![95415d4237b97c0402387702f250953](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\95415d4237b97c0402387702f250953.png)



### 04123: 马走日

dfs, http://cs101.openjudge.cn/practice/04123

思路：用回溯处理



代码：

```python
# pylint: skip-file
t = int(input())
dir=[(1,2),(2,1),(2,-1),(1,-2),(-1,-2),(-2,-1),(-2,1),(-1,2)]
def dfs(x,y,count):
    count+=1
    if count==n*m:
        global s
        s+=1
        return
    for dx,dy in dir:
          px,py=x+dx,y+dy
          if 0<=px<n and 0<=py<m and not visited[px][py]:
              visited[x][y]=True
              dfs(px,py,count)
              visited[x][y]=False
for _ in range(t):
    n,m,x,y=map(int,input().split())
    visited = [[False] * m for _ in range(n)]
    s=0
    dfs(x,y,0)
    print(s)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![34647f8c58d0e8df62f6e7820501eda](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\34647f8c58d0e8df62f6e7820501eda.png)



### sy316: 矩阵最大权值路径

dfs, https://sunnywhy.com/sfbj/8/1/316

思路：dfs回溯处理



代码：

```python
n,m=map(int,input().split())
a = [list(map(int,input().split())) for _ in range(n)]
import heapq
queue=[]
dir=[(-1,0),(1,0),(0,1),(0,-1)]
g = []
visited=[[False]*m for _ in range(n)]
def dfs(x,y,l,count):
    if x==n-1 and y==m-1:
        g.append((count,l+[(x+1,y+1)]))
        return
    for dx,dy in dir:
        px,py=x+dx,y+dy
        if 0<=px<n and 0<=py<m:
            if not visited[px][py]:
             visited[px][py]=True
             dfs(px,py,l+[(x+1,y+1)],count+a[x][y])
             visited[px][py]=False
visited[0][0]=True
dfs(0,0,[],0)
g.sort()
for index in g[-1][1]:
    print(*index)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![b64f352d16d162ee7058d7aa44db132](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\b64f352d16d162ee7058d7aa44db132.png)





### LeetCode62.不同路径

dp, https://leetcode.cn/problems/unique-paths/

思路：用组合数处理



代码：

```python
class Solution:
    import math
    def uniquePaths(self, m: int, n: int) -> int:
        return math.comb(m+n-2,m-1)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![78ec017b6948e2c8e39dd6e20b1db6a](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\78ec017b6948e2c8e39dd6e20b1db6a.png)



### sy358: 受到祝福的平方

dfs, dp, https://sunnywhy.com/sfbj/8/3/539

思路：dp处理



代码：

```python
n = input()[::-1]
import math
def ble(l):
    if l==0:
            return True
    for i in range(l):
        x = int(n[i:l][::-1])
        y = math.isqrt(x)
        if x==y**2 and y>0:
            if ble(i):
                return True
    return False
a=ble(len(n))
print('Yes' if a else 'No')
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![b2487b5931c79cbc75a0539589a3c44](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\b2487b5931c79cbc75a0539589a3c44.png)



## 2. 学习总结和收获

题目感觉基本能理解，但是还是不够熟练，每日选做在补，基本上弄完了。