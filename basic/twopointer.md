---
description: '#투 포인터'
---

# 투 포인터

## 백준 2003번 : 수들의 합 2

### 1. 단순 반복문 풀이

```text
count, sum=list(map(int, input().split(' ')))
a = list(map(int, input().split(' ')))

counting=0
temp=0

for i in range(count):
  temp=0
  for j in range(i, count):
    temp=temp + a[j]
    if(temp==sum):
      counting=counting+1
      break
    elif(temp>sum):
      break

print(counting)
```

### 2. 투 포인터 풀이

```text
n,m = map(int, input().split())
A=list(map(int, input().split()))

start=0
answer=0
end=0

while start <=end and end<=len(A):
    summ = sum(A[start:end])
    if summ==m:
        answer+=1
    if summ<=m:
        end+=1
    elif summ>m and start<end:
        start+=1

print(answer)
```
