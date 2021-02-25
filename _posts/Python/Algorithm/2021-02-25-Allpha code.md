---
title:  "알파 코드"
excerpt: "Algorithm"
categories:
  - Py_Algorithm
tags:
  - 3
last_modified_at: 2021-02-25

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math : true
---

- 문제 및 답 출처 : [링크](https://www.inflearn.com/course/%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EB%AC%B8%EC%A0%9C%ED%92%80%EC%9D%B4-%EC%BD%94%EB%94%A9%ED%85%8C%EC%8A%A4%ED%8A%B8/dashboard)

- 해당 링크에 가시면 훨씬 더 전문적인 해설 및 / 강의를 보실 수 있습니다. 

# 문제

**문제**  

![png](/assets/images/{Algorithm}/30_1.JPG)

**입력설명**

- 첫번째 줄에 숫자로 암호화된 코드가 입력된다. (코드는 0 으로 시작하지는 않는다. 코드의 길이는 최대 50이다.) 
- 0 이 입력되면 입력 종료를 의미한다.

**출력 설명**

- 입력된 코드를 알파벳으로 복원하는데에 몇가지 방법이 있는지 각 경우를 출력한다.
- 그 가짓수도 출력한다. 단어의 출력은 사전순으로 출력한다.

**입력 예제**

25114

**출력예제**

BEAAD

BEAN

BEKD

YAAD

YAN

YKD

6

# 내 해답

```python
import sys
sys.stdin = open('in2.txt','r')

N = input()

eng = list('ABCDEFGHIJKLMNOPQRSTUVWXYZ')
num = list(range(1,27))
dic = dict(zip(num,eng)) # 알파벳, 숫자가 대응되는 dictionary 생성
print(dic)
cnt = 0
# l 은 끝나는 지점이다.
# string 은 영어 단어
def DFS(l,string):
    global cnt
    if l > len(N) :
        return
    if l == len(N) : # 끝나는 지점이 N 이면 다 된것이다. 출력!
        print(string)
        cnt += 1
    else :
        if l == len(N)-1 :
            DFS(l + 1, string + dic[int(N[l:l + 1])])
        elif l == len(N)-2 :
            if (int(N[l:]) % 10 == 0 ):
                DFS(l+2,string + dic[int(N[l:])])
            elif (int(N[l:]) <= 26)  : # 즉 처음 두자리가 봐줄만 하면 괜찮다.
                DFS(l+2,string + dic[int(N[l:])]) # 시작되는 위치(또는 끝나는 위치라 해도 무방)가 변경
                DFS(l+1,string + dic[int(N[l:l+1])])
            else :
                DFS(l+1,string + dic[int(N[l:l+1])])
        else :
            if (int(N[l:l+2]) % 10 == 0 ):
                DFS(l+2,string + dic[int(N[l:l+2])])
            elif (int(N[l:l+2]) <= 26)  : # 즉 처음 두자리가 봐줄만 하면 괜찮다.
                DFS(l+2,string + dic[int(N[l:l+2])]) # 시작되는 위치(또는 끝나는 위치라 해도 무방)가 변경
                DFS(l+1,string + dic[int(N[l:l+1])])
            else :
                DFS(l+1,string + dic[int(N[l:l+1])])
DFS(0,'')
print(cnt)
```

- 너무 복잡하고 몇개 케이스에서 답이 달라져서 여기서 멈추었다.(나중에 더 풀어봐야할듯..)

# 다른 답

```python
import sys
sys.stdin=open("input.txt", "r")
def DFS(L, P):
    global cnt
    if L==n:
        cnt+=1
        for j in range(P):
            print(chr(res[j]+64), end='')
        print()
    else:
        for i in range(1, 27):
            if code[L]==i:
                res[P]=i
                DFS(L+1, P+1)
            elif i>=10 and code<[L]==i//10 and code[L+1]==i%10:
                res[P]=i
                DFS(L+2, P+1)

if __name__=="__main__":
    code=list(map(int, input()))
    n=len(code)
    code.insert(n, -1)
    res=[0]*(n+3)
    cnt=0
    DFS(0, 0)
    print(cnt)
```

- 내 접근방식은 '먼저 Case 를 보고 거기서부터 뜯어고치는 형식' 으로 하였는데, 점점 풀이를 보니 그런 방식보다는 '기준으로부터 시작' 하는것이 더 좋아보인다.
- 그래서 위처럼 for 문을 통해서 1~27 의 숫자를 뽑는다는 '조건' 을 통해서 for 문을 돌림과 동시에 같이 
- Case 를 하나하나 쪼개는게 아니라 '조건부터 적용' 하는것이 더 코드짜기도 편하고 좋다! 



# 내 해답 2

- 위 정답을 보고 바꾼 내 답.

```python
import sys
sys.stdin = open('in1.txt','r')
N = map(int,input())
N = list(N)
N.append(-1)
print(N)

eng = list('ABCDEFGHIJKLMNOPQRSTUVWXYZ')
num = list(range(1,27))
dic = dict(zip(num,eng)) # 알파벳, 숫자가 대응되는 dictionary 생성

# 스으윽 훑어가면서! 각 조건에 맞게 알파벳을 뽑아낸다.
# '조건 중심' 으로 훑어가는게 중요하다.
# 이떄 조건이란? 1~26 까지의 값 들중 같다면 그것을 추출하는것.
# Case 에 대해서 '일일히 조건을 적합시켜서 나눈다' 의 방법은 매우 복잡
# '조건에 대해서' 그거에 맞는 Case 를 나누어서 쪼갬.
cnt = 0
def DFS(l,string) :
    global cnt
    if l == len(N)-1 : # len 뒤에 쓸데없는게 있어서 그렇다..
        print(string)
        cnt += 1
    # 자 이제 '조건' 이 먼저 들어간다.
    # 훑어보았을 때에 조건에 맞으면 그냥 계~속 늘어나는거임
    # l 은 0부터 len(N)-1 까지 됩니다.
    for i in range(1,26):
        if N[l] == i : # 조건에 맞다! 그러면.?
            DFS(l+1,string+dic[i]) # 아래처럼 늘어나야지~
        if N[l] == i//10 and N[l+1]==i%10 and i >= 10 : #
            DFS(l+2,string+dic[i])
DFS(0,'')
print(cnt)
```

