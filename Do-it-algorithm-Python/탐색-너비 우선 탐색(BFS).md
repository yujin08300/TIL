너비 우선 탐색(BFS)
===========
> 너비 우선 탐색도 그래프를 완전 탐색하는 방법 중 하나로, 시작 노드에서
> 
> 출발해 시작 노드를 기준으로 ***가까운 노드를 먼저 방문***하면서 탐색하는 알고리즘이에요.


기능
---------------
그래프 완전 탐색


특징
-----------
FIFO(DFS는 FILO) 탐색

Queue(큐) 자료구조 이용


시간 복잡도(노드 수: V, 에지 수: E)
----------
O(V + E)

너비 우선 탐색은 **선입선출** 방식으로 탐색하므로 **큐**를 이용해 구현해요.  
또한 너비 우선 탐색은 탐색 시작 노드와 **가까운 노드를 우선 탐색**하므로  
목표 노드에 도착하는 경로가 여러 개일 때 **최단 경로를 보장**해요. 

너비 우선 탐색의 핵심 이론
----------
1. BFS를 시작할 노드를 정한 후 사용할 자료구조를 초기화해요.
   
<img width="1009" height="378" alt="image" src="https://github.com/user-attachments/assets/2e7f9603-83ef-4ebb-b904-5d9427559f91" />

T는 이미 방문했다는 것을 나타내요.  

2. 큐에서 노드를 꺼낸 후 꺼낸 노드의 인접 노드를 다시 큐에 삽입해요.  

<img width="1023" height="393" alt="image" src="https://github.com/user-attachments/assets/abb4c96b-a316-47f8-8e41-169184eee578" />
 

3. 큐 자료구조에 값이 없을 때까지 반복해요.

<img width="1104" height="407" alt="image" src="https://github.com/user-attachments/assets/e7d8f965-a4aa-48d6-93ef-a4c955716294" />

***코드 구현 해보기!***  

관련 문제:  

<https://www.acmicpc.net/problem/1260> 실버 2  

<https://www.acmicpc.net/problem/2178> 실버 1  

<https://www.acmicpc.net/problem/1167> 골드 2
