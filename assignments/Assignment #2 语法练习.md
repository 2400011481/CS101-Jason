# Assignment #2: 语法练习

Updated 0126 GMT+8 Sep 24, 2024

2024 fall, Complied by ==王梓航，物理学院==



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）课程网站是Canvas平台, https://pku.instructure.com, 学校通知9月19日导入选课名单后启用。**作业写好后，保留在自己手中，待9月20日提交。**

提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 263A. Beautiful Matrix

https://codeforces.com/problemset/problem/263/A



思路：找到非零元的位置，计算它和中心的曼哈顿距离即可



##### 代码

```python
  for i in range(5):
    a=list(map(int,input().split()))
    for j in range(5):
        if a[j]==1:
            print(abs(i-2)+abs(j-2))

```



代码运行截图 ==（至少包含有"Accepted"）==

![4fd79975faed85eafd02d25b8932c34](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\4fd79975faed85eafd02d25b8932c34.png)



### 1328A. Divisibility Problem

https://codeforces.com/problemset/problem/1328/A



思路：正常做即可



##### 代码

```python
N=int(input())
for i in range(N):
    t=input().split()
    a,b=int(t[0]),int(t[1])
    if a%b!=0:
        print(b-a%b)
    else:
        print(0) 

```



代码运行截图 ==（至少包含有"Accepted"）==

![9cbcd7621a34be7d65be399e3fd4db9](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\9cbcd7621a34be7d65be399e3fd4db9.png)



### 427A. Police Recruits

https://codeforces.com/problemset/problem/427/A



思路：计算前i个和的最小值进行判断。



##### 代码

```python
N = int(input())
a=list(map(int,input().split()))
for i in range(1,N):
    a[i]+=a[i-1]
a.sort()
if a[0]<0:
    print(-a[0])
else:
    print(0)

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![40a8e499fd1e6f540d42e84359c4ed2](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\40a8e499fd1e6f540d42e84359c4ed2.png)



### 02808: 校门外的树

http://cs101.openjudge.cn/practice/02808/



思路：一开始全部都有，然后选中的变成无即可



##### 代码

```python
#a,b=map(int,input().split())
g=[1 for _ in range(a+1)]
for i in range(b):
    c,d=map(int,input().split())
    g=g[0:c]+[0 for _ in range(d-c+1)]+g[d+1::]
print(sum(g)) 

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![e133aae87271b43fecab04e3ff92509](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\e133aae87271b43fecab04e3ff92509.png)



### sy60: 水仙花数II

https://sunnywhy.com/sfbj/3/1/60



思路：用整除找到各个位上的数，判断即可



##### 代码

```python
# a,b=map(int,input().split())
g=[]
for i in range(a,b+1):
  if i==(i//100)**3+((i//10)%10)**3+(i%10)**3:
    g.append(i)
if g!=[]:
    print(*g)
else:
    print('NO')

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![c47fc2f609409c6cb587bf0cdbcdb88](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\c47fc2f609409c6cb587bf0cdbcdb88.png)





### 01922: Ride to School

http://cs101.openjudge.cn/practice/01922/



思路：所求就是0时之后最早到的时间



##### 代码

```python
# import math
while True:
    N = int(input())
    if N==0:
        break
    f=100000000
    for i in range(N):
        a,b=list(map(int,input().split()))
        if b>=0:
            f=min(math.ceil(3600*(4.5/a)+b),f)
    print(f)

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![760fdd446d51e1419ae27c584f78474](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\760fdd446d51e1419ae27c584f78474.png)



## 2. 学习总结和收获

每日选做一直在跟进，进一步的学习感到自己的思路总是不够清晰，做题有些盲目，还没有想清楚就处理，结果并不理想。接下来的时间计划多做些题，锻炼自己的思维，提高自己的水平。