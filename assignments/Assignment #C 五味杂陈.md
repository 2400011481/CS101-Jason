# Assignment #C: 五味杂陈 

Updated 1148 GMT+8 Dec 10, 2024

2024 fall, Complied by <mark>王梓航，物理学院</mark>



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 1115. 取石子游戏

dfs, https://www.acwing.com/problem/content/description/1117/

思路：在b/a>=2时，先手取完最多或者少取一杯就可以模拟下一个环境的先手和后手，所以有必赢策略，否则进入下一步探究



代码：

```python
while True:
    a,b=sorted(list(map(int,input().split())))
    if a==0:
        break
    round=0
    while True:
        if b//a>=2 or b==a:
            if round%2==0:
                print('win')
            else:
                print('lose')
            break
        else:
            c = b
            b = a
            a = c-a
            round+=1
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![526efa5a568d751d9556252c8f7c296](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\526efa5a568d751d9556252c8f7c296.png)



### 25570: 洋葱

Matrices, http://cs101.openjudge.cn/practice/25570

思路：顺着按列剥到每一层里



代码：

```python
from collections import deque
n = int(input())
total=[0]*((n+1)//2)
for i in range(n):
    a = deque(map(int,input().split()))
    j = min(i,n-i-1)
    for t in range(j):
        total[t]+=a.pop()+a.popleft()
    total[j]+=sum(a)
print(max(total))
```



代码运行截图 ==（至少包含有"Accepted"）==

![7c7fca7e16b328af2e4e2c8b8f72ccd](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\7c7fca7e16b328af2e4e2c8b8f72ccd.png)



### 1526C1. Potions(Easy Version)

greedy, dp, data structures, brute force, *1500, https://codeforces.com/problemset/problem/1526/C1

思路：和维护最长单调递增数列类似，维护一个最优的喝的部分。如果能喝就加进来，否则就优化掉最低的。这样可以过C2



代码：

```python
import heapq
 
n = int(input())
a = list(map(int,input().split()))
total=0
queue=[]
result=0
for i in range(n):
    total+=a[i]
    heapq.heappush(queue,a[i])
    if total>=0:
        result+=1
    elif queue:
        total-=heapq.heappop(queue)
print(result)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![4689caa9efe4d83b9ea411b74380517](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\4689caa9efe4d83b9ea411b74380517.png)



### 22067: 快速堆猪

辅助栈，http://cs101.openjudge.cn/practice/22067/

思路：和答案中间懒删除基本类似，就是pop的时候记录下来，然后min出现的时候就丢掉。因为记录的是位置，可能会复杂一些



代码：

```python
import sys
import heapq
data = sys.stdin.read()
data = data.split()
a = []
b = []
j = 0
b_no=set([])
for index in data:
    if index=='pop':
        if b:
            n = heapq.heappop(b)
            b_no.add(-n)
    elif index=='min':
        if a and b:
            while True:
                m, n = heapq.heappop(a)
                if n not in b_no:
                    print(m)
                    heapq.heappush(a,(m,n))
                    break
    elif index!='push':
        heapq.heappush(a,(int(index),j))
        heapq.heappush(b,-j)
        j+=1
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>![a15394563d280879d3ec8dc46e6d113](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\a15394563d280879d3ec8dc46e6d113.png)





### 20106: 走山路

Dijkstra, http://cs101.openjudge.cn/practice/20106/

思路：模版题，正常做就可以了



代码：

```python
import heapq
dir=[(-1,0),(1,0),(0,1),(0,-1)]
m,n,p=map(int,input().split())
out=[input().split() for _ in range(m)]
for _ in range(p):
    x0,y0,x1,y1=map(int,input().split())
    if out[x0][y0]=='#' or out[x1][y1]=='#':
        print('NO')
        continue
    count = [[10 ** 6] * n for _ in range(m)]
    queue=[]
    heapq.heappush(queue,[0,x0,y0])
    while queue:
      total,x2,y2=heapq.heappop(queue)
      if (x2,y2)==(x1,y1):
          print(total)
          break
      if count[x2][y2]<total:
          continue
      for dx,dy in dir:
          px,py=x2+dx,y2+dy
          if 0<=px<m and 0<=py<n and out[px][py]!='#':
            s = total+abs(int(out[px][py])-int(out[x2][y2]))
            if count[px][py]>s:
              count[px][py]=s
              heapq.heappush(queue,[s,px,py])
    else:
        print('NO')
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![fcf40594d188d4f3fc27328125871d5](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\fcf40594d188d4f3fc27328125871d5.png)



### 04129: 变换的迷宫

bfs, http://cs101.openjudge.cn/practice/04129/

思路：

这个题参考的答案思路。我当时想的还是有些不妥，想的是把每一个周期的相互比较，相较而言就不是很好。

代码：

```python
import heapq
dir=[(-1,0),(1,0),(0,1),(0,-1)]
t = int(input())
for _ in range(t):
    r,c,k=map(int,input().split())
    map_out=[]
    x0,y0,x1,y1=-1,-1,-1,-1
    for i in range(r):
        list_out=input()
        if y0==-1:
            y0=list_out.find('S')
            if y0!=-1:
                x0=i
        if y1==-1:
            y1=list_out.find('E')
            if y1!=-1:
                x1=i
        map_out.append(list(list_out))
    time=0
    map_time=[[[False]*k for _ in range(c)] for _ in range(r)]
    queue=[]
    heapq.heappush(queue,[0,x0,y0])
    while queue:
        time,x2,y2=heapq.heappop(queue)
        if (x2,y2)==(x1,y1):
            print(time)
            break
        map_time[x2][y2][time%k]=True
        time+=1
        temp=time%k
        for dx,dy in dir:
            px,py=x2+dx,y2+dy
            if 0<=px<r and 0<=py<c and not map_time[px][py][temp]:
             if time%k==0 or map_out[px][py]!='#':
                    map_time[px][py][temp]=True
                    heapq.heappush(queue,[time,px,py])
    else:
        print('Oop!')
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![3c94a5bd5a4bec810fcdde33bdec779](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\3c94a5bd5a4bec810fcdde33bdec779.png)



## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>

每日选做在跟进。感觉考试还是很没有底。因为还没处理，这周计划梳理一下知识点，看一下往年题。期末还是要冲一冲。