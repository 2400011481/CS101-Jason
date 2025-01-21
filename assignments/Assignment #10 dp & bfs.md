# Assignment #10: dp & bfs

Updated 2 GMT+8 Nov 25, 2024

2024 fall, Complied by <mark>王梓航，物理学院</mark>



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### LuoguP1255 数楼梯

dp, bfs, https://www.luogu.com.cn/problem/P1255

思路：dp处理即可



代码：

```python
n = int(input())
a = [1,1]
for _ in range(n-1):
    a.append(a[-1]+a[-2])
print(a[-1])
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![311f57c9ade6b13fdc4db7e0779dac0](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\311f57c9ade6b13fdc4db7e0779dac0.png)



### 27528: 跳台阶

dp, http://cs101.openjudge.cn/practice/27528/

思路：每一个都是前面所有的和（包括走0级），所以就是2^（n-1）



代码：

```python
print(2**(int(input())-1))
```



代码运行截图 ==（至少包含有"Accepted"）==

![3cb2f2c9492ce1efb366769c66139c4](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\3cb2f2c9492ce1efb366769c66139c4.png)



### 474D. Flowers

dp, https://codeforces.com/problemset/problem/474/D

思路：就是最后一次可以吃1个也可以吃k个，然后用deque是怕内存爆掉，只保留前k个的结果



代码：

```python
import sys
from collections import deque
input = sys.stdin.read
data = input().split()
t,k=map(int,data[:2])
g = list(map(int,data[2:]))
a = deque([1]*k)
nums = [i+1 for i in range(k)]
for index in range(k,1+max(g)):
    a.append((a[-1]+a[0])%(10**9+7))
    a.popleft()
    nums.append((nums[-1]+a[-1])%(10**9+7))
for i in range(t):
    print((nums[g[2*i+1]]-nums[g[2*i]-1]+10**9+7)%(10**9+7))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![2aa8aeeffbfb55fab686b41c309b40b](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\2aa8aeeffbfb55fab686b41c309b40b.png)



### LeetCode5.最长回文子串

dp, two pointers, string, https://leetcode.cn/problems/longest-palindromic-substring/

思路：就是用最简单的方法实现的



代码：

```python

class Solution:
    def longestPalindrome(self, s: str) -> str:
      g=(-1,0,1)
      for i in range(len(s)):
        for j in range(2):
            left,right = i,i+j
            flag = False 
            while 0<=left<len(s) and 0<=right<len(s) and s[left]==s[right]:
                flag = True
                left-=1
                right+=1
            if flag:
                g = max(g,(right-left-2,left+1,right-1))
      return (s[g[1]:g[2]+1] if g[2]<len(s)-1 else s[g[1]:])
        


      
        
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![ff775916ff2b2207121a739be7041ed](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\ff775916ff2b2207121a739be7041ed.png)





### 12029: 水淹七军

bfs, dfs, http://cs101.openjudge.cn/practice/12029/

思路：改着改着就发毛了，最后改的和答案基本一样才过



代码：

```python
import sys
import heapq
data = sys.stdin.read()
data = data.split()
k = int(data[0])
data=data[1:]
results = []
for _ in range(k):
    flag = False
    m,n=map(int,data[:2])
    data = data[2:]
    a = [list(map(int,data[n*i:n*(i+1)])) for i in range(m)]
    data = data[m*n:]
    i,j,p=map(int,data[:3])
    data = data[3:]
    water_height=[[0]*n for _ in range(m)]
    for _ in range(p):
        x,y=map(int,data[:2])
        data=data[2:]
        if a[x-1][y-1]<=a[i-1][j-1]:
            continue
        else:
            water_height[x-1][y-1]=a[x-1][y-1]
            queue=[]
            heapq.heappush(queue,(x,y,a[x-1][y-1]))
            while queue:
                t,s,height=heapq.heappop(queue)
                for dx,dy in [(-1,0),(1,0),(0,1),(0,-1)]:
                    pt,ps=t+dx,s+dy
                    if 1<=pt<=m and 1<=ps<=n and a[pt-1][ps-1]<height and water_height[pt-1][ps-1]<height:
                        water_height[pt-1][ps-1]=height
                        heapq.heappush(queue,(pt,ps,height))
    results.append('Yes' if water_height[i-1][j-1]>0 else 'No')
sys.stdout.write('\n'.join(results) +'\n')
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![f840b7974ed8045f67e480657435bf6](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\f840b7974ed8045f67e480657435bf6.png)



### 02802: 小游戏

bfs, http://cs101.openjudge.cn/practice/02802/

思路：两个月前看书就学习过了答案的代码，但是这次实现+debug都花了我半个小时。



代码：

```python
import heapq
dir = [(-1,0),(0,1),(0,-1),(1,0)]
oppo = {0:3,3:0,1:2,2:1}
for i in range(1,12):
        w,h=map(int,input().split())
        if (w,h)==(0,0):
            break
        board = [[' ']*(w+2)]+[[' ']+list(input())+[' '] for _ in range(h)]+[[' ']*(w+2)]
        print('Board #{}:'.format(i))
        j=0
        while True:
            j+=1
            x1,y1,x2,y2=map(int,input().split())
            board[y2][x2]=' '
            if (x1,y1,x2,y2)==(0,0,0,0):
                break
            queue=[]
            heapq.heappush(queue,[0,-1,x1,y1])
            visited=[[False]*(w+2) for _ in range(h+2)]
            visited[y1][x1]=True
            while queue:
                count,an,x0,y0=heapq.heappop(queue)
                visited[y0][x0]=True
                if (x0,y0)==(x2,y2):
                    print('Pair {}: {} segments.'.format(j,count))
                    break
                for num,(dx,dy) in enumerate(dir):
                    px,py=x0+dx,y0+dy
                    if 0<=px<=w+1 and 0<=py<=h+1 and board[py][px]==' ' and oppo[num]!=an and not visited[py][px]:
                        if num==an:
                            heapq.heappush(queue,[count,an,px,py])
                        else:
                            heapq.heappush(queue,[count+1,num,px,py])
            else:
                print('Pair {}: impossible.'.format(j))
            board[y2][x2]='X'
        print('')
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![2aaab9a4ced43b12790ed0b0436a7c1](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\2aaab9a4ced43b12790ed0b0436a7c1.png)



## 2. 学习总结和收获

感觉题目基本上能理解，最后两题花的时间比较多。感觉自己花的时间主要都在debug，真的有点头大。