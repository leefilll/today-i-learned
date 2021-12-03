## 우선순위 큐(Priority Queue)

일반적으로 큐(Queue)는 FIFO 구조
우선순위 큐는 들어간 순서에 상관없이 우선순위가 높은 데이터가 먼저 나오는 큐
힙(Heap)을 이용하여 구현

> 일반 배열(연결 리스트)로 구현할 경우, 삭제는 O(1), 삽입은 O(n)의 시간복잡도가 소요됨. 그러나 힙으로 구현할 경우 삭제와 삽입 모두 O(logn)안에 가능함

### 연산

- **삽입**

  - 우선순위 큐에 추가
  - 완전이진트리의 마지막 노드에 새로운 노드를 추가
  - 추가된 노드를 부모노드와 비교하며 교환
  - 더이상 교환이 되지 않을 때까지 반복
  - 최악의 경우 루트노드까지 올라가야 하므로 힙트리의 높이인 log(n+1)에 따라서 시간복잡도는 **O(logn)**

- **삭제**

  - 우선순위 큐에서 가장 우선순위가 높은 요소를 삭제하고 반환
  - 루트노드가 가장 우선순위가 높은(최대 힙이던, 최소 힙이던) 요소이기에 삭제
  - 완전이진트리의 마지막 노드를 루트노드로 가져옴
  - 자식노드 중 더 큰(최대 힙) 값 혹은 더 작은(최소 힙) 값과 교환
  - 더이상 교환이 되지 않을 때까지 반복
  - 삽입과 똑같이 시간복잡도는 **O(logn)**

- **조회**
  - 우선순위 큐에서 가장 우선순위가 높은 요소를 반환