# Assignment #B: Dec Mock Exam大雪前一天

Updated 1649 GMT+8 Dec 5, 2024

2024 fall, Complied by <mark>王梓航，物理学院</mark>



**说明：**

1）⽉考： AC3<mark>（请改为同学的通过数）</mark> 。考试题⽬都在“题库（包括计概、数算题目）”⾥⾯，按照数字题号能找到，可以重新提交。作业中提交⾃⼰最满意版本的代码和截图。

2）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### E22548: 机智的股民老张

http://cs101.openjudge.cn/practice/22548/

思路：先找到最大和最小，如果先最小后最大就直接大减小；否则分成三部分，左侧，中间，右侧，递归处理中间，两侧分别处理即可



代码：

```python
a = list(map(int,input().split()))
def search(a):
    if len(a)<=1:
        return 0
    M=max(a)
    m=min(a)
    xM=a.index(M)
    xm=len(a)-a[::-1].index(m)-1
    if xM>=xm:
        return M-m
    else:
        yM=min(a[:xM+1])
        ym=max(a[xm:])
        z = search(a[xM+1:xm])
        zM=M-yM
        zm=ym-m
        return max(z,zM,zm)
print(search(a))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![3eda82ba5a4ef9f1133bb206e778d74](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\3eda82ba5a4ef9f1133bb206e778d74.png)



### M28701: 炸鸡排

greedy, http://cs101.openjudge.cn/practice/28701/

思路：和群里讨论的类似，就是大的就一直放里面，小的可以看成液体随意切割。考场上有一个n忘了改成len(a)就WA了，感觉是最可惜的一道题。可能再多花一分钟debug就成了。



代码：

```python
import bisect

n,k=map(int,input().split())
a = sorted(map(int,input().split()))
while True:
    time=sum(a)/k
    i = bisect.bisect_right(a,time)
    if i==len(a):
        print('%.3f'%time)
        break
    else:
        k-=len(a)-i
        a = a[:i]
```



代码运行截图 ==（至少包含有"Accepted"）==

![6ddbf6a5840251da36331b43810f2fe](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\6ddbf6a5840251da36331b43810f2fe.png)



### M20744: 土豪购物

dp, http://cs101.openjudge.cn/practice/20744/

思路：基本思路就是维护两个dp，一个是截止为i的最大值（可以删去一个），一个是截止为i的最大和（不可以删去）。这是考场上写的，当时怕超时做了优化，先把所有整数相邻的加起来，减小后面的计算量。这里-2,-2,-2会出问题，应该是要特殊考虑的，但是测试数据没有，导致AC了。应该加两句就好了。考场上写的比较乱。



代码：

```python
a = list(map(int,input().split(',')))
n = len(a)
total=0
a_sum=[]
for index in range(n):
    if a[index]<0:
        if total!=0:
            a_sum.append(total)
        total=0
        a_sum.append(a[index])
    else:
        total+=a[index]
a_sum.append(total)
n = len(a_sum)
s=0
p=0
e=[]
for index in range(n):
    x1=s+a_sum[index]
    x2=p
    s = max(x1,x2)
    e.append(s)
    p=max(0,p+a_sum[index])
print(max(e))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![e24d13c9a60e23a4690f9e36cf56b9f](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\e24d13c9a60e23a4690f9e36cf56b9f.png)



### T25561: 2022决战双十一

brute force, dfs, http://cs101.openjudge.cn/practice/25561/

思路：正常dfs处理即可，只是很麻烦



代码：

```python
import bisect

n,m=map(int,input().split())
price=[[-1]*m for _ in range(n)]
at_least=[[] for _ in range(m)]
less=[[] for _ in range(m)]
for i in range(n):
    get=input().split()
    for index in get:
        t,s=map(int,index.split(':'))
        price[i][t-1]=s
for i in range(m):
    get = input().split()
    for index in get:
      a,b=map(int,index.split('-'))
      at_least[i].append(a)
      less[i].append(b)
result = float('inf')
def get_to(a,y):
    if n==y:
        global result
        total=sum(a)
        total-=total//300*50
        for i,index in enumerate(a):
            if at_least[i]:
                j = bisect.bisect_right(at_least[i],index)
                if j>0:
                    total-=max(less[i][:j])
        result = min(result,total)
        return
    for i,index in enumerate(price[y]):
        if index!=-1:
            a[i]+=index
            get_to(a,y+1)
            a[i]-=index
a=[0]*m
get_to(a,0)
print(result)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![2c0a83aa44fe748bb5cebdc9e1f7ccc](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\2c0a83aa44fe748bb5cebdc9e1f7ccc.png)



### T20741: 两座孤岛最短距离

dfs, bfs, http://cs101.openjudge.cn/practice/20741/

思路：一个bfs找第一个岛，另一个从第一个岛找第二个岛。基本都是按套路来，只是visited可以共享，感觉是唯一一个优化



代码：

```python
import heapq
dir = [(-1,0),(1,0),(0,1),(0,-1)]
n = int(input())
a = [list(map(int,list(input()))) for _ in range(n)]
m = len(a[0])
first=set([])
for i in range(n):
    for j in range(m):
        if a[i][j]==1:
            visited=[[False]*m for _ in range(n)]
            visited[i][j]=True
            queue=[]
            heapq.heappush(queue,(i,j))
            first.add((i,j))
            while queue:
                x,y=heapq.heappop(queue)
                for dx,dy in dir:
                    px,py=x+dx,y+dy
                    if 0<=px<n and 0<=py<m and not visited[px][py] and a[px][py]==1:
                        visited[px][py]=True
                        first.add((px,py))
                        heapq.heappush(queue,[px,py])
            queue = []
            for p, q in first:
                heapq.heappush(queue, [0, p, q])
            while queue:
                count, x, y = heapq.heappop(queue)
                count += 1
                for dx, dy in dir:
                    px, py = x + dx, y + dy
                    if 0 <= px < n and 0 <= py < m and not visited[px][py]:
                        visited[px][py] = True
                        heapq.heappush(queue, [count, px, py])
                        if a[px][py] == 1:
                            print(count-1)
                            exit(0)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![77ff88745aa17ce76d9a3d541010451](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\77ff88745aa17ce76d9a3d541010451.png)



### T28776: 国王游戏

greedy, http://cs101.openjudge.cn/practice/28776

思路：

最后一个相当于所有人左手除以他的左右手的积，所以要选取积最大的。前面的相当于也是除以左右手，但是积更小，只用看最后一个。

代码：

```python
n = int(input())
a = [tuple(map(int,input().split())) for _ in range(n+1)]
def key1(x):
    return x[0]*x[1]
a = [a[0]]+sorted(a[1:],key=key1)
s=1
for i in range(n):
    s*=a[i][0]
print(s//a[-1][1])
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![11f7f5d707c40ac2bc22390463aceef](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\11f7f5d707c40ac2bc22390463aceef.png)



## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>

考场上心态还是有点爆炸。第二题一开始没弄出双dp，第三题思路是对的结果有一个n要修成len(a)忘了弄，整个人慌了神。幸亏第四题迅速AC，第五题一看太麻烦没做，后悔没看第六题，当然考场上第六题可能也看不出来（不过我觉得第三题的贪心更难想一些，第六题如果乘法不好想还能取对数成加减法，更加好想）。最后回头做了第二题。第三题感觉很可惜，思路是对的。时间规划确实不好弄