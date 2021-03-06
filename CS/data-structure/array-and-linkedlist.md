## Array와 LinkedList

### Array

- 번호(인덱스)와 번호에 대응하는 데이터로 이루어진 자료구조
- 일반적으로는 같은 종류의 데이터들이 순차적으로 저장됨
- 값의 인덱스가 곧 배열의 시작점으로부터 값이 저장되어 있는 상대적인 위치가 됨
- 인덱스를 알고 있으면 O(1)의 시간복잡도(즉, random access가 허f용됨)
- 삭제나 삽입의 과정에서 `shift`의 과정이 생기기 때문에, 최악의 경우 시간복잡도가 O(n)이 됨
- static memory allocation(컴파일 시점에 할당)
- stack 영역에 메모리 할당

### Linked List

- 각각의 데이터는 자신의 값(value)와 다음에 나올 값의 주소(next)를 갖고 있음
- 삭제와 삽입의 시간복잡도는 O(1)
- 그러나 특정 인덱스에 대해서 조회하는 값이 Array와 다르게 연속적인 메모리 주소가 아니라서 그 데이터를 찾기 위해 O(n)이라는 시간복잡도가 소요됨
- dynamic memory allocation(런타임 시점에 할당)
- heap 영역에 메모리 할당

### 정리

- 데이터 조회가 중요할 경우, Array 사용
- 데이터 수정이 중요할 경우, Linked List 사용
