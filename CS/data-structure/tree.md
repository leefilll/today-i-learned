## Tree 구조

그래프의 일종, 여러 노드가 하나의 노드를 가리킬 수 없는 구조
노드(Node)와 간선(Edge)로 이루어진 자료 구조

- **루트 노드(root node)**: 최상위 노드
- **부모 노드(parent node)**: 노드 A가 노드 B를 가리킬 때 A가 B의 부모 노드
- **자식 노드(child node)**: 노드 A가 노드 B를 가리킬 때 B가 A의 자식 노드
- **잎 노드(leaf node)**: 자식 노드가 없는 노드
- **내부 노드(internal node)**: 잎 노드가 아닌 노드

### 트리 구조의 특성

- 사이클이 존재할 수 없음(사이클이 있다면, 트리 구조가 아닌 그래프)
- 모든 노드는 자료형으로 표현 가능함
- 루트에서 한 노드로 가는 경로는 유일함
- 노드의 개수가 N개라면, 간선은 (N-1)개
- 재귀 형태로 쉽게 구현 가능함(단, 트리의 높이에 비례한 스택 공간이 필요)

### 트리 순회(Tree traversal)

트리 구조에서 각각의 노드를 정확히 한 번만, 체계적인 방법으로 방문하는 과정

- **전위 순회(pre-order)**
  각 루트를 순차적으로 먼저 방문하는 방식

  1. 노드를 방문
  2. 왼쪽 서브 트리를 전위 순회
  3. 오른쪽 서브 트리를 전위 순회

  > 전위 순회는 깊이 우선 순회(depth-first traversal)라고도 함

  ```
  preorder(node):
    print node.value
    if node.left ≠ null then preorder(node.left)
    if node.right ≠ null then preorder(node.right)
  ```

- **중위 순회(in-order)**
  왼쪽 서브 트리를 방문 후 루트를 방문하는 방식

  1. 왼쪽 서브 트리를 중위 순회
  2. 노드를 방문
  3. 오른쪽 서브 트리를 중위 순회

  > 중위 순회는 대칭 순회(symmetric)라고도 함

  ```
  inorder(node)
    if node.left  ≠ null then inorder(node.left)
    print node.value
    if node.right ≠ null then inorder(node.right)
  ```

- **후위 순회(post-order)**
  왼쪽 서브 트리부터 하위를 모두 방문 후 루트를 방문하는 방식

  1. 왼쪽 서브 트리를 후위 순회
  2. 오른쪽 서브 트리를 후위 순회
  3. 노드를 방문

  ```
  postorder(node)
    if node.left  ≠ null then postorder(node.left)
    if node.right ≠ null then postorder(node.right)
    print node.value
  ```

- **레벨 순회(level-order)**
  루트부터 계층 별로 방문하는 방식

  > 레벨 순회는 너비 우선 순회(breadth-first traversal)라고도 함

### 사용

- **중위 순회**
  이진 탐색 트리의 탐색에 사용됨. 이진 탐색 트리에서 모든 왼쪽 서브 트리는 현재 노드 N보다 작고, 모든 오른쪽 서브 트리는 N보다 크거나 같음. 따라서 중위 순회로 방문할 시, 모든 노드를 순서대로 방문할 수 있음

- **전위 순회**
  전위 표기법의 식의 값 계산에 사용 할 수 있음
  전위 표기법 식 \* + 2 3 4 (중위 표기법으로는 (2 + 3) \* 4)을 계산하는 법

  | **전위 표기식** | **스택** |
  | :-------------: | :------: |
  |   \* + 2 3 4    |    -     |
  |    \* + 2 3     |    4     |
  |     \* + 2      |   3 4    |
  |      \* +       |  2 3 4   |
  |       \*        |   5 4    |
  |     **답**      |  **20**  |

### 예시

![250px-Sorted_binary_tree svg](https://user-images.githubusercontent.com/38246878/143965358-4bd5d6d6-3696-4c3b-919e-555870cc33b1.png)

- 전위 순회: F > B > A > D > C > E > G > I > H
- 중위 순회: A > B > C > D > E > F > G > H > I
- 후위 순회: A > C > E > D > B > H > I > G > F
- 레벨 순회: F > B > G > A > D > I > C > E > H
