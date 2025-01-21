# Assignment #7: Nov Mock Exam立冬

Updated 1646 GMT+8 Nov 7, 2024

2024 fall, Complied by <mark>王梓航 物理学院</mark>



**说明：**

1）⽉考： AC4 。考试题⽬都在“题库（包括计概、数算题目）”⾥⾯，按照数字题号能找到，可以重新提交。作业中提交⾃⼰最满意版本的代码和截图。

2）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### E07618: 病人排队

sorttings, http://cs101.openjudge.cn/practice/07618/

思路：

分成两组排序处理

代码：

```python
n = int(input())
a = []
b = []
for i in range(n):
    x,y = input().split(' ')
    y = int(y)
    if y>=60:
        a.append((-y,i,x))
    if y<60:
        b.append((i,x))
a.sort()
b.sort()
for index in a+b:
    print(index[-1])
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![6698c961e248c3da841452d243ef02b](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\6698c961e248c3da841452d243ef02b.png)



### E23555: 节省存储的矩阵乘法

implementation, matrices, http://cs101.openjudge.cn/practice/23555/

思路：

正常矩阵计算即可

代码：

```python
n,m1,m2=map(int,input().split())
a = [list(map(int,input().split())) for _ in range(m1)]
b = [list(map(int,input().split())) for _ in range(m2)]
c = [[0]*n for _ in range(n)]
for index in a:
    for t in b:
        if index[1]==t[0]:
            c[index[0]][t[1]]+=index[2]*t[2]
for i in range(n):
    for j in range(n):
        if c[i][j]!=0:
            print(i,j,c[i][j])
```



代码运行截图 ==（至少包含有"Accepted"）==

![7c51d45396ac7d9bd0f38c38d146195](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\7c51d45396ac7d9bd0f38c38d146195.png)



### M18182: 打怪兽 

implementation/sortings/data structures, http://cs101.openjudge.cn/practice/18182/

思路：

对于每个时刻，找到前m个处理

代码：

```python
n = int(input())
for _ in range(n):
    a,b,c=map(int,input().split())
    h = {}
    for __ in range(a):
        x,y=map(int,input().split())
        h.setdefault(x,[])
        h[x].append(y)
    for index in h.keys():
        g = sorted(h[index],reverse=True)
        g = g[:b]
        h[index] = sum(g)
    l = sorted(h.items())
    for i in l:
        c -= i[1]
        if c<=0:
            print(i[0])
            break
    else:
        print('alive')
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![7c51d45396ac7d9bd0f38c38d146195](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\7c51d45396ac7d9bd0f38c38d146195.png)



### M28780: 零钱兑换3

dp, http://cs101.openjudge.cn/practice/28780/

思路：

递归地处理

代码：

```python
n,m=map(int,input().split())
p = sorted(list(map(int,input().split())))
s =[0]+[10**6]*m
for index in range(m):
    g=[s[index+1-t] for t in p if index+1-t>=0]
    if g:
        s[index+1]=min(g)+1
print(s[m] if s[m]<10**6 else -1)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![40beb58b77308c7ab85ae9d230ce024](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\40beb58b77308c7ab85ae9d230ce024.png)



### T12757: 阿尔法星人翻译官

implementation, http://cs101.openjudge.cn/practice/12757

思路：

million thousand 断开处理，hundred 特殊处理即可

代码：

```python
a = input().split(' ')
b={'negative':-1, 'zero':0, 'one':1, 'two':2, 'three':3, 'four':4, 'five':5, 'six':6, 'seven':7, 'eight':8, 'nine':9, 'ten':10,
   'eleven':11, 'twelve':12, 'thirteen':13, 'fourteen':14, 'fifteen':15, 'sixteen':16, 'seventeen':17, 'eighteen':18, 'nineteen':19,
   'twenty':20, 'thirty':30, 'forty':40, 'fifty':50, 'sixty':60, 'seventy':70, 'eighty':80, 'ninety':90, 'hundred':100, 'thousand':1000, 'million':1000000}
s = 0
c = 0
flag = True
if a[0]=='negative':
    flag = False
    a=a[1:]
for index in a:
    if index in ['thousand','million']:
        s +=c*b[index]
        c = 0
    elif index =='hundred':
        c*= b[index]
    else:
      c += b[index]
s+=c
print(s if flag else -s)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![5470011971f662164c03755121b77d0](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\5470011971f662164c03755121b77d0.png)



### T16528: 充实的寒假生活

greedy/dp, cs10117 Final Exam, http://cs101.openjudge.cn/practice/16528/

思路：

递归正常处理即可

代码：

```python
n = int(input())
h = {}
for _ in range(n):
    x,y = map(int,input().split())
    h.setdefault(y,[])
    h[y].append(x)
dp=[0]*62
for index in range(61):
    if index in h.keys():
        g = h[index]
        dp[index+1]=max([dp[i] for i in h[index]])+1
    dp[index+1]=max(dp[index],dp[index+1])
print(dp[61])
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![4b3c9f75b97d8f1c1cab608da91e436](C:\Users\王\Documents\WeChat Files\wxid_1sdyw7c25zqz22\FileStorage\Temp\4b3c9f75b97d8f1c1cab608da91e436.png)



## 2. 学习总结和收获

最近准备期中考试，每日选做只做了部分。周四上午考试，所以是后来自己计时完成的月考。结果是在两个中等题上出了问题，主要就是第三题，做完后对答案发现应该是一样的，只是我是先对key排序再算每个时刻的总和，顺序不同，但是就WA了。这个比较折磨，而且自己找不到反例。感觉还是要多做些题，多总结一下套路。