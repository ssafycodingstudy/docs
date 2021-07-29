# Stack / Queue / Deque


# Stack이란?

## 개념

![Stack%20Queue%20Deque/Stack.png](Stack%20Queue%20Deque/Stack.png)

- **LIFO(후입선출**) 방식의 자료구조

## 특징

- 오직 맨 위에 추가(push)할 수 있고, 맨 위에 것만 나갈(pop) 수 있다.
- 가장 위에 있는 자료를 가리키는 것이 top
- top을 통해 삽입하는 연산을 **push**, 삭제하는 연산을 **pop**
- stack underflow : 비어있는 스택에서 원소를 추출할때
- stack overflow : 스택이 넘치는 경우
- 삽입/삭제 시간복잡도 : O(1)

## 장점

- 데이터의 삽입/삭제가 빠름 O(1)

## 단점

- 탐색 하려면 엘리먼트 하나하나 꺼내서 옮겨가야함(비효율적)
- 맨 위의 원소만 접근 가능

## 연산

List를 Stack 처럼!

- init

    ```jsx
    st = []
    st = list()
    ```

- push

     

    ```jsx
    st.append(1) # li = [1]
    st.append(2) # li = [1, 2]
    ```

- pop

    ```jsx
    # st = [1, 2]
    top = st.pop()
    print(top) # 2
    ```

- peek

    ```jsx
    st = [1, 2, 3, 4]
    top = st[-1]
    print(top) # 4
    ```

## 활용예시

- 재귀 알고리즘 (괄호 검사)
- 역추적 (역순 문자열 만들기)
- DFS

```jsx
def DFS_with_adj_list(graph, root):
    visited = []
    stack = [root]

    while stack:
        n = stack.pop()
        if n not in visited:
            visited.append(n)
            stack += graph[n] - set(visited)
    return visited

print(BFS_with_adj_list(graph_list, root_node))
```

현재 방문한 노드에 연결된 노드를 방문하는 깊이 우선 탐색에는 한 방향 작업을 하는 Stack이 적합

# Queue 란?

## 개념

![Stack%20Queue%20Deque/Queue.png](Stack%20Queue%20Deque/Queue.png)

- **FIFO(선입선출)** 방식의 자료구조

## 특징

- 한쪽 끝에서 삽입 작업, 다른 쪽 끝에서 삭제 작업이 양쪽으로 이루어진다.
- 삭제연산만 수행되는 곳을 front, 삽입연산만 이루어지는 곳을 rear
- 큐의 rear에서 이루어지는 삽입연산을 인큐(enQueue)
- 큐의 front에서 이루어지는 삭제연산을 디큐(dnQueue)

## 단점

- 큐를 list 타입으로 입력, 출력할 때는 list.pop(0)의 시간 복잡도가 O(N)이라 비효율적인 코드가 만들어진다.
- 이를 위해, collections 라이브러리의 deque를 사용해 시간을 절약

# Deque란?

## 개념

- 큐가 선입선출(FIFO) 방식으로 작동한다면 양방향 큐로 작동하는 것이 **deque!**
- 앞, 뒤 양쪽 방향에서 엘리먼트(element) 추가하거나 제거

## 특징

- 크기가 가변적 (선언 후 변경 가능)
- 삭제할때 큐는 pop(), 데큐는 popleft()
- 삽입/삭제/탐색(index) 시간복잡도 : O(1)

## 장점

- 데이터의 삽입/삭제가 빠름 O(1)
- 앞, 뒤에서 데이터 삽입/삭제 가능
- index로 임의 원소 접근 가능
- new 원소 삽입시, 메모리를 재할당후 복사하지 않고 새로운 단위의 메모리 블록 할당하여 삽입

## 단점

- 중간에 위치한 데이터로의 접근(삽입,삭제) 어려움

## 연산

- init

    ```jsx
    from _collection import deque
    q = deque()
    ```

- push

    ```jsx
    q.append(1)
    q.append(2)
    print(q) # [1, 2]
    ```

- pop

    ```jsx
    popped = q.popleft()
    print(popped) # 1
    ```

- peek

    ```jsx
    q = [2, 3, 4, 5]
    head = q[0]
    print(head) # 2
    ```

## 활용예시

- 앞과 뒤에서 삽입/삭제가 자주 일어나는 경우
- 데이터의 개수가 가변적일 경우
- 데이터 검색을 거의 하지 않는 경우 (랜덤 요소에 접근할 때)
- 데이터가 입력된 시간 순서대로 처리해야하는 상황
- 콜센터 대기 순서
- BFS

    ```jsx
    from collections import deque

    def BFS_with_adj_list(graph, root):
        visited = []
        queue = deque([root])

        while queue:
            n = queue.popleft()
            if n not in visited:
                visited.append(n)
                queue += graph[n] - set(visited)
        return visited
      
    print(BFS_with_adj_list(graph_list, root_node))
    ```

    - 노드를 방문하면서 인접한 노드 중 방문 하지 않은 노드의 정보만 큐에 넣어 먼저 큐에 있던 노드부터 방문

## 사용법

![Stack%20Queue%20Deque/Deque.png](Stack%20Queue%20Deque/Deque.png)

- deque.rotate(num)

    양수 값 or 음수 값을 파라미터로 제공하여 데크를 좌, 우로 회전

    ```jsx
    # Contain 1, 2, 3, 4, 5 in deq
    deq = deque([1, 2, 3, 4, 5])

    deq.rotate(1)
    print(deq)
    # deque([5, 1, 2, 3, 4])

    deq.rotate(-1)
    print(deq)
    # deque([1, 2, 3, 4, 5])
    ```