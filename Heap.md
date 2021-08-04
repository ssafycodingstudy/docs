## Heap

- 힙은 최댓값 및 최솟값을 찾아내는 연산을 빠르게 하기위해 고안된 완전이진트리(complete binary tree)를 기본으로 하는 자료구조다.
- 힙은 다음과 같은 속성을 만족한다.
  - A가 B의 부모노드(parent node)이면, A의 키(key)값과 B의 키값 사이에는 대소관계가 성립한다.
  - 이때 자식노드의 값이 부모노드의 값보다 항상 작은 힙을 최대 힙 (Max Heap)이라고 한다.
  - 이때 자식노드의 값이 부모노드의 값보다 항상 큰 힙을 최소 힙 (Min Heap)이라고 한다.



![25335F4357A4226509](https://user-images.githubusercontent.com/50684682/128113524-0b249480-1e74-4298-83d6-8440eb9b97d5.png)





- 키값의 대소관계는 오로지 부모노드와 자식노드 간에만 성립하며, 특히 형제 사이에는 대소관계가 정해지지 않는다.

- 힙 자료구조는 우선순위 큐(Priority Queue)를 구현하기 위해서 사용한다.
- 힙을 실제로 구현하는 문제보다는 힙의 원리를 통해 구현된 우선순위 큐를 사용하는 문제가 코딩테스트에서 많이 출제된다. 우선순위 큐도 따로 구현하기보다는 라이브러리를 활용한다. 



## 우선순위 큐(Priority Queue)

- 우선순위 큐는 우선순위가 가장 높은 데이터를 가장 먼저 출력하는 자료구조이다.

| 자료구조                    | 추출되는 데이터             |
| --------------------------- | --------------------------- |
| 스택(Stack)                 | 가장 나중에 삽입된 데이터   |
| 큐(Queue)                   | 가장 먼저 삽입된 데이터     |
| 우선순위 큐(Priority Queue) | 가장 우선순위가 높은 데이터 |



- 우선순위 큐는 배열이나 LinkedList로도 구현할 수 있지만, 삽입할 때 걸리는 시간 복잡도가 힙 기반이 훨씬 빠르기 때문에 힙으로 구현한다.

| 우선순위 큐 구현 방식 | 삽입 시간 | 삭제 시간 |
| --------------------- | --------- | --------- |
| 배열                  | O(N)      | O(1)      |
| LinkedList            | O(N)      | O(1)      |
| 힙                    | O(logN)   | O(logN)   |



- 우선순위 큐는 데이터를 우선순위에 따라 처리하고 싶을 때 사용한다. 예를 들면 여러 개의 데이터를 자료구조에 넣었다가 가치가 높은 데이터부터 꺼내서 확인해야 하는 경우 우선순위 큐 자료구조를 이용하면 효과적이다.

- 우선순위 큐를 구현할 때는 내부적으로 최대 힙 (Max Heap) 또는 최소 힙 (Min Heap)을 이용하는데, **최소 힙을 이용하는 경우**는 '**값이 작은 데이터가 먼저 삭제**'되고 최대 힙을 이용하는 경우는 '**값이 큰 데이터가 먼저 삭제**'된다.

  ※ 파이썬과 자바의 경우는 최소 힙을 이용해서 우선순위 큐 라이브러리가 구현되어 있으며, C++의 경우 최대 힙을 이용해서 우선순위 큐 라이브러리가 구현되어 있다.
  
  

## 우선순위 큐 라이브러리 활용법

#### 자바

- 선언

```java
import java.util.PriorityQueue; //import

//int형 priorityQueue 선언 (우선순위가 낮은 숫자 순)
PriorityQueue<Integer> priorityQueue = new PriorityQueue<>();

//int형 priorityQueue 선언 (우선순위가 높은 숫자 순)
PriorityQueue<Integer> priorityQueue = new PriorityQueue<>(Collections.reverseOrder());

//String형 priorityQueue 선언 (우선순위가 낮은 숫자 순)
PriorityQueue<String> priorityQueue = new PriorityQueue<>(); 

//String형 priorityQueue 선언 (우선순위가 높은 숫자 순)
PriorityQueue<String> priorityQueue = new PriorityQueue<>(Collections.reverseOrder());


```

- 사용

```java
PriorityQueue<Integer> priorityQueue = new PriorityQueue<>();//int형 priorityQueue 선언

priorityQueue.offer(2);     // priorityQueue에 값 2 추가
priorityQueue.offer(1);     // priorityQueue에 값 1 추가
priorityQueue.offer(3);     // priorityQueue에 값 3 추가
System.out.println(priorityQueue.peek());       // 출력값 : 1

```



#### 파이썬

- 선언 및 사용

```python
import heapq # import

q = []

# q에 데이터를 집어넣는 경우.
heapq.heappush(q, 2)
heapq.heappush(q, 1)
heapq.heappush(q, 3)

# q에서 데이터를 추출하는 경우.
print(heapq.heappop(q)) # 출력값 : 1
```

- 파이썬에서 우선순위 큐가 필요한 경우 PriorityQueue 혹은 heapq 라이브러리를 사용하면 되는데, 일반적으로 heapq가 더 빠르게 동작하기 때문에 수행 시간이 제한된 상황에서는 heapq를 사용하는 것이 더 낫다.



#### 최소 힙을 최대 힙처럼 활용

- 자바

```java
PriorityQueue<Integer> priorityQueue = new PriorityQueue<>();//int형 priorityQueue 선언

priorityQueue.offer(-2);     // priorityQueue에 값 2 추가
priorityQueue.offer(-1);     // priorityQueue에 값 1 추가
priorityQueue.offer(-3);     // priorityQueue에 값 3 추가
System.out.println(-(priorityQueue.peek()));       // 출력값 : 3

```



- 파이썬

```python
import heapq # import

q = []

data = [2, 1, 3]

# q에 데이터를 집어넣는 경우.
heapq.heappush(q, -data[0])
heapq.heappush(q, -data[1])
heapq.heappush(q, -data[2])

# q에서 데이터를 추출하는 경우.
print(-(heapq.heappop(q))) # 출력값 : 3
```



- 최소 힙의 데이터 중 가장 작은 값부터 출력되기 때문에, 가장 큰 값부터 출력하고 싶다면 넣을때 부호를 바꿔서 넣어주고 ('-' 추가), 뺄 때 부호를 ('-' 추가) 다시 넣어준다면 최대 힙처럼 사용할 수 있다.



> 참고자료
>
> https://coding-factory.tistory.com/603
>
> https://chanhuiseok.github.io/posts/ds-4/ : 우선순위 큐를 구현하는 과정이 구현되어 있음.

