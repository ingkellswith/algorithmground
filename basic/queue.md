---
description: '#큐 #구현 #자료 구조 #시뮬레이션'
---

# 큐

## 백준 1966번 : 프린터큐

### 1. 풀이

```text
test_case = int(input())
for _ in range(test_case):
  n, m = list(map(int, input().split(' ')))
  queue = list(map(int, input().split(' ')))
  queue = [(i, idx) for idx, i in enumerate(queue)]
  count = 0
  while True:
    if queue[0][0] == max(queue, key=lambda x: x[0])[0]:
      count += 1
      if queue[0][1] == m:
        print(count)
        break
      else:
        queue.pop(0)
    else:
      queue.append(queue.pop(0))
```

