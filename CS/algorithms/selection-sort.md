## 선택 정렬

주어진 배열 중에서 최솟값을 찾아 배열의 맨 앞에 위치한 값과 교체하여 정렬하는 방법
정렬된 이후의 배열에 대해서 위의 과정을 반복하여 끝까지 정렬

- 제자리 정렬(in-place sorting)
  입력 배열 외에 추가적인 메모리를 요구하지 않음
- 1회전을 수행하고 나면 가장 작은 원소가 맨 앞에 오게 됨. k번째 회전에서는 k번째로 작은 원소가 k번째로 오게됨
- 최고, 최악, 평균 셋 다 O(n^2)의 시간복잡도
- 원소의 순서가 보장되지 않음

### 구현 (C 언어)

```c
void selection_sort (vector<int> & list) {
  for (int i = 0 ; i < list.size() ; i++) {
    for (int j = 0 ; j < list.size() ; j++) {
      if (list[i] < list[j]) {
        swap(list[i], list[j]);
      }
    }
  }
}

```
