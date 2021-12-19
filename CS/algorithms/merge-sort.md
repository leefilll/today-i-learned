## 합병 정렬

합병 정렬은 **분할 정복(divide and conquer) 방법**을 통해 정렬함

- 분할 정복 방법: 문제를 작은 2개의 문제로 분리하여 각각을 해결한 다음, 결과를 모아서 원래의 문제를 해결하는 정략
  대개, 재귀 호출을 이용하여 구현

- 분할(Divide), 정복(Conquer), 결합(Combine)의 과정을 거침

  - 분할: 입력 배열을 같은 크기 2개의 부분 배열로 분할
  - 정복: 부분 배열을 정렬함. 재귀호출을 통해서 부분 배열이 충분히 작도록 구현
  - 결합: 정렬된 부분 배열들을 하나의 배열에 합병

- 계속 분할 하여 정렬하기 때문에 최악, 최고, 평균일 경우 O(n log n)의 시간복잡도를 지님
- 배열을 복사해야 하므로 공간복잡도는 O(n)
- 원소의 순서가 보장되는 **안정정렬**
- 레코드를 연결 리스트로 구현할 경우, 데이터의 이동은 매우 작아지고, 제자리 정렬(in-place sorting)이 가능함
- 크기가 큰 레코드를 정렬할 경우, 합병 정렬이 다른 정렬보다 효율적

### 정렬 과정

![merge-sort-concepts](https://user-images.githubusercontent.com/38246878/146649467-90782e73-c5ba-430b-985a-37ea61f352ac.png)

1. 리스트의 길이가 0 또는 1이면 이미 정렬된 것으로 봄
2. 정렬되지 않은 리스트를 절반으로 잘라 비슷한 크기의 두 부분 리스트로 나눔
3. 각 부분 리스트를 재귀적으로 합병 정렬
4. 두 부분 리스트를 다시 하나의 정렬된 리스트로 합병

### 구현 (C++)

```cpp
void merge (vector<int> &list, int left, int mid, int right) {
  vector<int> sorted_list(list.size());

  int i = left, j = mid+1, idx = left;

  while(i <= mid && j <= right) {
    if (list[i] <= list[j]) {
      sorted_list[idx++] = list[i++];
    } else {
      sorted_list[idx++] = list[j++];
    }
  }
  while(i <= mid) {
    sorted_list[idx++] = list[i++];
  }

  while(j <= right) {
    sorted_list[idx++] = list[j++];
  }

  for (int l = left ; l <= right ; l++) {
    list[l] = sorted_list[l];
  }
}

void partition (vector<int> &list, int left, int right) {
  int mid;

  if (left < right) {
    mid = (left + right) / 2;
    partition(list, left, mid);
    partition(list, mid + 1, right);
    merge(list, left, mid, right);
  }
}
```
