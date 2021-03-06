BFS(Breadth First Search) & DFS(Depth First Search)
===
(참고 자료 : 패스트캠퍼스 이준희님의 알고리즘 강의)

# 1. BFS vs DFS

너비 우선 탐색 : BFS(Breadth First Search)
- 정점들과 같은 레벨에 있는 노드들을 먼저 탐색하는 방식

깊이 우선 탐색 : DFS(Depth First Search)
- 정점의 자식들을 먼저 탐색하는 방식

BFS 방식: A - B - C - D - G - H - I - E - F - J
    한 단계씩 내려가면서, 해당 노드와 같은 레벨에 있는 노드들 (형제 노드들)을 먼저 순회함

DFS 방식: A - B - D - E - F - C - G - H - I - J
    한 노드의 자식을 타고 끝까지 순회한 후, 다시 돌아와서 다른 형제들의 자식을 타고 내려가며 순화함

![bfsdfs](https://user-images.githubusercontent.com/55550753/134816883-1a382d84-da7d-4b29-836b-6b9b3d4ccfc5.PNG)

# 2. 파이썬으로 BFS, DFS 그래프 표현

파이썬 딕셔너리와 리스트로 그래프 표현 가능  

### bfs 그래프
![bfsgraph](https://user-images.githubusercontent.com/55550753/135262999-2cdb65ef-5d28-4cea-a16f-7b0b32452e05.PNG)  

### dfs 그래프
![dfsgraph](https://user-images.githubusercontent.com/55550753/135262845-4d338735-9618-4333-9ec1-4295dc830553.PNG)

한 노드에 연관되어 있는 노드들을 모두 적는다.  

```text
graph = dict()

graph['A'] = ['B', 'C']
graph['B'] = ['A', 'D']
graph['C'] = ['A', 'G', 'H', 'I']
graph['D'] = ['B', 'E', 'F']
graph['E'] = ['D']
graph['F'] = ['D']
graph['G'] = ['C']
graph['H'] = ['C']
graph['I'] = ['C', 'J']
graph['J'] = ['I']

print(graph)
```
아래는 결과값이다.  
```text
{'A': ['B', 'C'],
 'B': ['A', 'D'],
 'C': ['A', 'G', 'H', 'I'],
 'D': ['B', 'E', 'F'],
 'E': ['D'],
 'F': ['D'],
 'G': ['C'],
 'H': ['C'],
 'I': ['C', 'J'],
 'J': ['I']}
```

bfs, dfs모두 그래프 표현은 같다.   
하지만 알고리즘 구현에서 bfs는 need_visit queue를 사용하는 반면,  
dfs는 need_visit stack을 사용하는 것이 특징이다.  

# 3. BFS 탐색 순서 알고리즘 구현

### bfs 알고리즘에서의 visited큐, need_visit큐 사용 예시

![bfsqueue](https://user-images.githubusercontent.com/55550753/134817145-d7a3b525-c928-404e-8ecf-3b96da889fa8.PNG)  

visited queue와 need_visit queue(**두 개의 큐**)와  
need_visit.pop(0)으로 뽑은 node(**한개의 temp**)를 사용해서 bfs 탐색 순서 알고리즘을 구현할 수 있다.  


```text
def bfs(graph, start_node):
    visited = list()
    need_visit = list()
    
    need_visit.append(start_node)
    
    while need_visit:
        node = need_visit.pop(0)
        if node not in visited:
            visited.append(node)
            need_visit.extend(graph[node])
    
    return visited

print(bfs(graph, 'A'))
```
결과값
```text
['A', 'B', 'C', 'D', 'G', 'H', 'I', 'E', 'F', 'J']
```
# 4. DFS 탐색 순서 알고리즘 구현  

visited queue(**큐**), need_visit stack(**스택**)과
need_visit.pop()으로 뽑은 node(**한개의 temp**)를 사용해서 dfs 탐색 순서 알고리즘을 구현할 수 있다.  


```text
def dfs(graph, start_node):
    visited, need_visit = list(), list()
    need_visit.append(start_node)
    
    while need_visit:
        node = need_visit.pop()
        if node not in visited:
            visited.append(node)
            need_visit.extend(graph[node])
    
    return visited

print(dfs(graph, 'A'))
```
결과값
```text
['A', 'C', 'I', 'J', 'H', 'G', 'B', 'D', 'F', 'E']
```

# 5. 시간 복잡도

일반적인 BFS, DFS 시간 복잡도
- 노드 수: V
- 간선 수: E
위 코드에서 while need_visit 은 V + E 번 만큼 수행함
- 시간 복잡도: O(V + E)