# 1. 트리 Tree

#
### 1) 트리

비선형 자료구조 — 계층적 구조

- 우선순위큐 - Heap

최댓값, 최솟값을 빠르게 찾기 위한 완전 이진트리

힙은 정렬된 구조가 아님. 상/하 관계를 보장

삽입, 삭제 O(logN)

탐색 O(N)

- 이진탐색트리(Binary Search Tree) - TreeMap, TreeSet

정렬된 트리

모든 왼쪽 자식들 ≤ n < 모든 오른쪽 자식들

특정 key를 기준으로 사전순으로 정렬된 데이터를 가져올 때 사용

삽입, 삭제, 탐색 O(logN)  
  
#
### 2) 구조  

1. 데이터와 연결상태를 저장할 클래스 공간 ( = 노드) 생성
2. 각각의 노드들에 값 저장
3. 노드간 연결 상태 정의

```java
//노드
public class Node{
	Object data;
	Node left;
	Node right;
}
```
#
### 3) 용어

루트(root) : 트리 구조 중 최상위에 존재하는 노드

노드(node) : 트리 각각의 구성요소

간선(edge) : 노드와 노드를 연결하는 선

형제 노드(sibling) : 같은 레벨의 노드

부모 노드(parent node) : 한 노드를 기준으로 바로 상위의 노드

자식 노드(child node) : 한 노드를 기준으로 바로 하위의 노드

레벨(level) : 트리 각각의 층 ( 루트 노드의 레벨 — 0 ), 간선의 수

높이(heigh) : 트리 중 최고 레벨

차수(degree) : 연결된 자식 노드의 수

서브트리: 부모노드와 연결된 간선을 끊었을때 생성되는 트리


#
### 4) 순회

- 전위(pre-order)
- 중위(in-order)
- 후위(post-order)
- 레벨

1. 전위 순회 pre-order

    루트 노드를 먼저 순회한 후, 왼쪽 하위 → 오른쪽 하위 순으로 순회

    현재 노드 → 왼쪽 가지 → 오른쪽 가지

    ```java
    	private void dfsByPreOrder(int current) {
    		// 현재 노드 처리
    		System.out.print(nodes[current] + " ");
    		// 왼쪽 자식 노드 방문
    		if (current * 2 <= lastIndex)
    			dfsByPreOrder(current * 2);
    		// 오른쪽 자식 노드 방문
    		if (current * 2 + 1 <= lastIndex)
    			dfsByPreOrder(current * 2 + 1);
    	}
    ```

1. 중위 순회 in-order

    왼쪽 가장 하위 노드를 먼저 순회한 후,  상위 노드 → 오른쪽 하위 순으로 순회

    왼쪽 가지 → 현재 노드 → 오른쪽 가지

    ```java
    	public void dfsByInOrder(int current) {
    		// 왼쪽 자식 노드 방문
    		if (current * 2 <= lastIndex)
    			dfsByInOrder(current * 2);
    		// 현재 노드 처리
    		System.out.print(nodes[current] + " ");
    		// 오른쪽 자식 노드 방문
    		if (current * 2 + 1 <= lastIndex)
    			dfsByInOrder(current * 2 + 1);
    	}
    ```

2. 후위 순회 post-order

    왼쪽 가장 하위 노드를 먼저 순회한 후, 오른쪽 하위 노드 → 상위노드 순으로 순회

    왼쪽 가지 → 오른쪽 가지 → 현재 노드

    ```java
    	public void dfsByPostOrder(int current) {
    		// 왼쪽 자식 노드 방문
    		if (current * 2 <= lastIndex)
    			dfsByInOrder(current * 2);
    		// 오른쪽 자식 노드 방문
    		if (current * 2 + 1 <= lastIndex)
    			dfsByInOrder(current * 2 + 1);
    		// 현재 노드 처리
    		System.out.print(nodes[current] + " ");
    	}
    ```

3. 레벨 순회

    큐를 이용하여 레벨별로 순회

    ```java
    Queue<Integer> queue = new LinkedList<Integer>();
    queue.offer(1); // 루트 인덱스 저장

    int cur = 0;
    while (!queue.isEmpty()) {
    	cur = queue.poll();
    	System.out.println(nodes[cur]);
    	if (cur * 2 <= lastIndex)
    		queue.offer(cur * 2);
    	if (cur * 2 + 1 <= lastIndex)
    		queue.offer(cur * 2 + 1);
    }
    ```
#
### 5) 이진탐색트리 TreeSet, TreeMap

탐색시 균형이 깨지면(한쪽으로 치중) O(N)의 속도를 가질 수 있기 때문에 레드-블랙트리 사용

- 레드-블랙 트리

![image](https://user-images.githubusercontent.com/55391944/129137565-2fedc381-6139-4e15-a171-f1e3f9948273.png)

1. 노드는 레드 혹은 블랙 중의 하나이다.
2. 루트 노드는 블랙이다.
3. 모든 리프 노드들(빈노드)은 블랙이다.
4. 레드 노드의 자식노드 양쪽은 언제나 모두 블랙이다. (즉, 레드 노드는 연달아 나타날 수 없으며, 블랙 노드만이 레드 노드의 부모 노드가 될 수 있다)
5. 어떤 노드로부터 시작되어 그에 속한 하위 리프 노드에 도달하는 모든 경로에는 리프 노드를 제외하면 모두 같은 개수의 블랙 노드가 있다.

루트 노드부터 가장 먼 잎노드 경로까지의 거리 < 가장 가까운 잎노드 경로까지의 거리 * 2

 →  균형

최단 경로는 모두 블랙 노드로만 구성되어 있다고 했을 때
최장 경로는 블랙 노드와 레드 노드가 번갈아 나오는 것
다섯 번째 속성에 따라서, 모든 경로에서 블랙 노드의 수가 같다고 했기 때문에 존재하는 모든 경로에 대해 최장 경로의 거리는 최단 경로의 거리의 두 배 이상이 될 수 없다.

- TreeSet

이진 트리를 기반으로한 Set 컬렉션

부모값과 비교해서 낮은 것은 왼쪽 자식 노드에, 높은 것은 오른쪽 자식 노드에 정렬

```java
TreeSet<E> treeSet = new TreeSet<E>();
treeSet.add(e);

Iterator<Integer> it = treeSet.descendingIterator();
while(it.hasNext()) {
	Integer ss = it.next();
	System.out.println(ss);
}
		
NavigableSet<Integer> ds = treeSet.descendingSet();
it = ds.iterator();
while(it.hasNext()) {
	Integer ss = it.next();
	System.out.println(ss);
}

// x < 90
SortedSet<Integer> a90 = treeSet.headSet(90);
it = a90.iterator();
while (it.hasNext()) {
	System.out.print(it.next() + " ");
}
// x >= 85
SortedSet<Integer> b85 = ts.tailSet(85,true);
it = b85.iterator();
while(it.hasNext()) {
	System.out.print(it.next() + " ");
}

// 85 < x <= 95
SortedSet<Integer> a8595 = ts.subSet(85, false, 95, true);
it = a8595.iterator();
while(it.hasNext()) {
	System.out.print(it.next() + " ");
}

```

![image](https://user-images.githubusercontent.com/55391944/129137917-dd425b21-6409-4092-9014-123bcabadb71.png)


![image](https://user-images.githubusercontent.com/55391944/129137948-5f287196-c6e2-4559-84cd-2b57b37698ab.png)

![image](https://user-images.githubusercontent.com/55391944/129137974-ab6588ea-ab22-4b24-a3b8-593acf9a0486.png)

![image](https://user-images.githubusercontent.com/55391944/129137998-5ec52f2b-3206-4a89-a73f-934296221398.png)


- TreeMap

이진 트리를 기반으로 한 Map.Entry 컬렉션

부모 키값과 비교해서 키 값이 낮은 것은 왼쪽 자식 노드에, 키 값이 높은 것은 오른쪽 자식 노드에 정렬

```java
TreeMap<K, V> treeMap = new TreeMap<>();
treeMap.put(k, v);

// 키값으로 내림차순해서 출력하는 코드 1
NavigableMap<Integer, String> deMap = treeMap.descendingMap();
Set<Map.Entry<Integer, String>> des = deMap.entrySet();
for (Entry<Integer, String> entry : des) {
	System.out.println("학생 : " + entry.getValue() + "\t" + entry.getKey() + "점");
}
System.out.println();

		
// 키값으로 내림차순해서 출력하는 코드 2
NavigableSet<Integer> keyset = treeMap.descendingKeySet();
Iterator<Integer> it = keyset.iterator();
while (it.hasNext()) {
	Integer key = it.next();
	String value = scores.get(key);
	System.out.println("학생 : " + value + "\t" + key + "점");
}
System.out.println();

// 범위 검색
TreeMap<String, Integer> treeMap = new TreeMap<String, Integer>();
		
treeMap.put("apple", new Integer(10));
treeMap.put("forever", new Integer(60));		
treeMap.put("description", new Integer(40));
treeMap.put("ever", new Integer(50));
treeMap.put("zoo", new Integer(10));
treeMap.put("base", new Integer(20));
treeMap.put("guess", new Integer(70));
treeMap.put("cherry", new Integer(30));
		
System.out.println("[c~f 사이의 단어 검색]");
// c부터 f까지라서
// 시작이 f로 된 거 까지만 (뒤에 덧붙여진 내용이 있는 forever는 출력되지 x
NavigableMap<String, Integer> reangeMap = treeMap.subMap("c", true, "f", true);
for(Map.Entry<String, Integer> entry : reangeMap.entrySet()) {
	System.out.println(entry.getKey() + "-" + entry.getValue() + "페이지");
}
```

![image](https://user-images.githubusercontent.com/55391944/129138024-c4352720-b1a4-42fb-a9b8-fe2c4a879eef.png)

> 출처
[https://sabarada.tistory.com/145](https://sabarada.tistory.com/145)
[https://velog.io/@cyhse7/TreeSet-TreeMap](https://velog.io/@cyhse7/TreeSet-TreeMap)
