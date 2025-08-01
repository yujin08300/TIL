깊이 우선 탐색(DFS)
==============
> 그래프 완전 탐색 기법 중 하나예요.
> 
> 그래프 시작 노드에서 출발하여 탐색할 한 쪽 분기를 정하여 최대 깊이까지 탐색을
>  
> 마친 후 다른 쪽 분기로 이동하여 다시 탐색을 수행하는 알고리즘이에요.


기능
-------
그래프 완전 탐색


특징
-------
재귀 함수로 구현해요.  

스택 자료구조(FILO: 먼저 들어온 데이터가 나중에 나간다)를 이용해요.  


시간 복잡도(노드 수: V, 에지 수: E)
---------------------
O(V+E)  

깊이 우선 탐색은 실제 구현 시 재귀 함수를 이용하므로 스택 오버플로에    

유의해야 해요. 응용 문제는 단절점 찾기, 단절선 찾기, 사이클 찾기, 위상 정렬    

등이 있어요. 


**스택 오버플로: 재귀 호출이 너무 많이 반복되면,**  

**스택 공간이 초과되어 프로그램이 강제 종료되는 현상**


핵심 이론
--------------
한 번 방문한 노드를 다시 방문하면 안 되므로 노드 방문 여부를 체크할 배열이  

필요하며, 그래프는 인접 리스트로 표현하겠습니다. 그리고 DFS의 탐색 방식은 후  

입선출 특성을 가지므로 스택을 사용하여 설명하겠습니다.  

***여기서는 설명의 편의를 위해 스택을 사용했지만, DFS 구현은 스택보다는  
스택 성질을 갖는 재귀 함수로 많이 구현해요.***

<img width="1044" height="375" alt="image" src="https://github.com/user-attachments/assets/5e6cc6c8-6019-4036-b10f-e790ef9b4e78" />


<img width="1003" height="404" alt="image" src="https://github.com/user-attachments/assets/d9a4a20e-f3ac-4562-af0d-4aa4826df682" />



대상 노드의 인접 노드를 스택에 삽입하는 과정에서 이미 다녀간 노드(2, 3)인지 확인해야

해요. 이미 다녀간 노드는 재삽입하지 않는 것이 핵심이에요. 

삽입하기 전에 방문 여부를 체크하고 삽입한 후에 방문 배열에 T, F를 써넣어요.  


<img width="1342" height="486" alt="image" src="https://github.com/user-attachments/assets/ed30d141-a855-476c-a452-bd512cf01223" />


스택에 노드를 삽입할 때 방문 배열을 체크하고, 스택에서 노드를 뺄 때 탐색 순서에  

기록하며 인접 노드를 방문 배열과 대조하여 살펴요.  


<img width="238" height="213" alt="image" src="https://github.com/user-attachments/assets/9a70db84-56c5-4fd3-a4ec-ab8dd133eb6d" />

1->2->3까지 깊이 탐색 했다가 나오면서 4탐색, 5탐색

***코드 구현 해보기!***  

관련 문제:   

[연결 요소의 개수](https://github.com/yujin08300/TIL/blob/main/Do-it-algorithm-Python/%EA%B9%8A%EC%9D%B4%20%EC%9A%B0%EC%84%A0%20%ED%83%90%EC%83%89-%EC%8B%A4%EC%A0%84%EB%AC%B8%EC%A0%9C-%EC%97%B0%EA%B2%B0%20%EC%9A%94%EC%86%8C%EC%9D%98%20%EA%B0%9C%EC%88%98-%EB%B0%B1%EC%A4%80%2011724.md)    
<https://www.acmicpc.net/problem/11724> 실버 2  

<https://www.acmicpc.net/problem/2023> 골드 5  

<https://www.acmicpc.net/problem/13023> 골드 5


