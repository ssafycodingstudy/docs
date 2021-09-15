# DFS BFS 중 적합한 문제 찾기

![DFSBFS](https://media.vlpt.us/images/lucky-korma/post/e2ef7ac3-14e6-42e7-a768-224c5f773e29/R1280x0-3.gif)

기본적으로 두 방식 모두 조건 내의 모든 노드를 검색한다는 점에서 시간 복잡도는 동일함.

#### DFS(깊이 우선 탐색)

1. 모든 정점을 방문하고자 하는 경우
2. 경로의 특징을 저장해야 되는 경우 
   - ex)경로에 같은 숫자가 있으면 안된다. 경로를 저장해야한다.
3. 검색 대상 그래프가 매우 큰 경우

#### BFS(깊이 우선 탐색)

1. 최단 거리를 구해야 할 경우 
   - BFS의 경우 가까운 노드부터 탐색하기 때문에 경로 탐색시 먼저 찾아지는 경우가 해답
2. 규모가 작고 시작 지점과 종료지점이 가까울 경우

DFS와 BFS - https://www.acmicpc.net/problem/1260

BFS - https://www.acmicpc.net/problem/14496

DFS - https://www.acmicpc.net/problem/1520

시간비교

안전 지역 - https://www.acmicpc.net/problem/2468

섬의 개수 - https://www.acmicpc.net/problem/4963

