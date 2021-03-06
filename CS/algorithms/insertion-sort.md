## 삽입 정렬

삽입 정렬은 자료 배열의 모든 요소를 앞에서부터 차례대로 이미 정렬된 배열 부분과 비교하여 자신의 위치를 찾아 삽입하면서 정렬하는 알고리즘

- 앞에서부터 이미 정렬된 배열 부분과 비교하여 자신의 위치를 찾아 삽입
- 매 순서 마다 해당 원소를 삽입할 수 있는 위치를 찾아 해당 위치에 넣음
- 최선의 경우 O(n), 최악의 경우 O(n^2), 평균 O(n^2)
  최선의 경우는 모두 정렬이 되어 있는 경우(한 번씩 밖에 비교를 하지 않음), 최악의 경우는 역순일 경우(모든 비교를 거쳐야 함)

### 특징

- 안전한 정렬 방법(순서가 바뀌지 않음)
- 알고리즘 자체가 매우 간단
- 대부분의 레코드가 정렬된 상태일 경우 매우 효율적일 수 있음
- 그러나, 많은 레코드의 이동이 있고 크기가 큰 데이터의 경우 비효율적

### 구현 (Python)

```python
def insert_sort(x):
  # key는 1번 인덱스 시작함
  for i in range(1, len(x)):
    j = i - 1
    key = x[i]
    while x[j] > key and j >= 0:
      x[j+1] = x[j]
      j -= 1
    x[j+1] = key
  return x
```

### 구현 (C++)

```cpp
void insertion_sort (vector<int> & list) {
  int i, j;
  for (i = 1 ; i < list.size() ; i++) {
    int current = list[i];
    for (j = i - 1 ; j >= 0 ; j--) {
      if (list[j] > current) {
        list[j + 1] = list[j];
      } else {
        break;
      }
    }

    list[j + 1] = current;
  }
}
```
