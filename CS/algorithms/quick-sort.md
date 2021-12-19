## Quick Sort

다른 원소와 비교만으로 정렬을 수행하는 **비교 정렬 알고리즘**

- n개의 데이터를 정렬할 때, 최악의 경우 O(n^2)번 비교를 수행하고, 평균적으로 O(nlogn)번의 비교를 수행
- 만약, 같은 값이 있는 경우 정렬 이후의 순서가 초기 순서와 달라질 수 있는 **불안정 정렬**에 속함
  > `5(1), 5(2), 3, 2, 1`을 정렬하면 `1, 2, 3, 5(2), 5(1)`이 됨

### 알고리즘

퀵 정렬은 **분할 정복(divide and conquer) 방법**을 통해 정렬함

1. 리스트 가운데서 하나의 원소를 고름(피벗)
2. 피벗 앞에는 피벗보다 값이 작은 원소들이 오고, 피벗 뒤에는 피벗보다 값이 큰 모든 원소들이 오도록 피벗을 기준으로 데이터를 둘로 나눔(분할)
3. 분할된 두 개의 작은 리스트에 대해 재귀(recursion)적으로 이 과정을 반복함. 재귀는 각 리스트의 크기가 0이나 1이 될 때까지 반복함

> 재귀 호출이 한 번 진행될 때 마다, 최소한 하나의 원소는 최종적으로 위치가 정해짐

### 특징

- 프로그래밍 언어의 대다수의 기본 정렬 알고리즘이 이 퀵소트를 구현하고 있음
- pivot의 선택이 성능에 큰 영향을 미침. pivot 값을 기준으로 작은 값들과 큰 값들이 동일하게 분할되면 가장 좋은 성능.
- 정렬하고자 하는 데이터의 크기가 작을 때 재귀의 비용이 더 많이 듬<br/>그래서 원소의 개수에 따라 다른 정렬을 혼합하여 사용
- 공간 복잡도의 경우에는 구현 방법에 따라 달라짐. 일반적으로는 입력 배열이 차지하는 메모리만을 사용하는 in-place sorting 방식으로 구현하여 O(1)의 공간복잡도를 갖게 됨.

- 순열이나 역순의 경우 매우 느린 속도를 보임(피봇이 최소나 최댓값이라면 모든 원소를 비교해야 하므로)

### 퀵 정렬이 빠른 이유

- CPU 캐시의 히트율이 높음
  > 지역성(Locality)은 CPU가 짧은 시간 범위 내에 일정 구간의 메모리 영역을 반복적으로 액세스하는 경향을 말함. 퀵 정렬의 경우, 합병 정렬과 다르게 피봇을 이용하기는 하지만, 데이터가 존재하는 위치는 변하지 않음.
- 매 단계에서 적어도 1개의 원소가 자기 자리를 찾게 됨(pivot)

### 구현 (Python)

```python
def quick_sort(arr):
  if len(arr) <= 1:
    return arr
  pivot = arr[len(arr) // 2]
  lesser_arr, equal_arr, greater_arr = [], [], []
  for num in arr:
    if num < pivot:
      lesser_arr.append(num)
    elif num > pivot:
      greater_arr.append(num)
    else:
      equal_arr.append(num)
  return quick_sort(lesser_arr) + equal_arr + quick_sort(greater_arr)
```

이 경우에는 간단하지만, 매번 재귀호출마다 새로운 리스트를 생성하여야 하므로, 메모리 사용 측면에서 비효울적임.

### 구현(Python, in-place sorting)

```python
def quick_sort(arr):
  def sort(low, high):
    if high <= low:
      return
    mid = partition(low, high)
    sort(low, mid - 1)
    sort(mid, high)

  def partition(low, high):
    pivot = arr[(low + high) // 2]
    while low <= high:
      while arr[low] < pivot:
        low += 1
      while arr[high] > pivot:
        high -= 1
      if low <= high:
        arr[low], arr[high] = arr[high], arr[low]
        low, high = low + 1, high - 1
    return low

  return sort(0, len(arr) - 1)

```

### 구현 (C++)

```cpp
void quick_sort (vector<int> & list, int head, int tail) {
  if (head >= tail) return;

  int pivot = head;
  int left = pivot + 1;
  int right = tail;

  while(left <= right) {
    while(left <= tail && list[left] <= list[pivot]) {
      left++;
    }
    while(right > head && list[right] >= list[pivot]) {
      right--;
    }

    if (left > right) {
      swap(list[pivot], list[right]);
    } else {
      swap(list[right], list[left]);
    }
  }

  quick_sort(list, head, right - 1);
  quick_sort(list, right + 1, tail);
}
```
