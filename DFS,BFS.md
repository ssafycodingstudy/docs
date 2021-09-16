[TOC]

# DFS/BFS

## 그래프 표현방식

- 그래프를 표현하는 방식은 인접 행렬, 인접 리스트의 두 가지 방식이 있다.
- 특정한 노드와 연결된 모든 인접 노드를 순회해야 하는 경우, 인접 리스트 방식이 인접 행렬 방식에 비해 메모리 공간의 낭비가 적다.



## Depth First Search(깊이 우선 탐색)

- DFS는 Depth-First Search, 깊이 우선 탐색이라고도 부르며, 그래프에서 깊은 부분을 우선적으로 탐색하는 알고리즘이다. 

- 그래프는 node와 edge로 표현되며, 이때 노드를 vertex라고도 한다. DFS를 수행할 때는 데이터의 개수가 N개인 경우 O(N)의 시간이 소요된다.



```python
#DFS 메서드 정의
def dfs(graph, vertex, visited):  
# 현재 노드를 방문 처리  
	visited[vertex] = True  
	print(vertex, end=' ')  
	# 현재 노드와 연결된 다른 노드를 재귀적으로 방문  
	for i in graph[vertex]:    
		if not visited[i]:      
			dfs(graph, i, visited)
```





## Breadth First Search(너비 우선 탐색)

- BFS는 Breadth First Search, 너비 우선 탐색이라는 의미를 가진다. 가까운 노드부터 탐색하는 알고리즘이다. 
- 큐 자료구조에 기초한다는 점에서 구현이 간단. O(N)의 시간이 소요된다. 
- 실제 수행 시간은 DFS보다 좋은 편이다. DFS보다는 BFS 구현이 조금 더 빠르게 동작한다.



```python
from collections import deque
#BFS 메서드 정의
def bfs(graph, start, visited):  
    # 큐(Queue) 구현을 위해 deque 라이브러리 사용  
    queue = deque([start])  
    # 현재 노드를 방문 처리  
    visited[start] = True  
    # 큐가 빌 때까지 반복  
    while queue:    
        # 큐에서 하나의 원소를 뽑아 출력    
        v = queue.popleft()    
        print(v, end=' ')    
        # 해당 원소와 연결된, 아직 방문하지 않은 원소들을 큐에 삽입    
        for i in graph[v]:      
            if not visited[i]:        
                visited[i] = True
                queue.append(i)
```



## 예제

```python
#각 노드가 연결된 정보를 리스트 자료형으로 표현(2차원 리스트)
graph = [
    [],
    [2, 3, 8],#1
    [1, 7],#2
    [1, 4, 5],#3
    [3, 5],#4
    [3, 4],#5
    [7],#6
    [2, 6, 8],#7
    [1, 7]#8
]

# 각 노드가 방문된 정보를 리스트 자료형으로 표현(1차원 리스트)
visited = [False] * 9
# 정의된 함수 호출
dfs(graph, 1, visited)
bfs(graph, 1, visited)
```



![Cap 2021-09-16 00-31-19-142](https://user-images.githubusercontent.com/50684682/133463648-423c8064-cca6-4b2e-8665-abfabe647476.jpg)



## 결과

```
dfs : 1 2 7 6 8 3 4 5
bfs : 1 2 3 8 7 4 5 6 
```



## DFS vs BFS

|           |      DFS       |       BFS        |
| :-------: | :------------: | :--------------: |
| 동작 원리 |      스택      |        큐        |
| 구현 방법 | 재귀 함수 이용 | 큐 자료구조 이용 |

