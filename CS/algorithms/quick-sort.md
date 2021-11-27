## Quick Sort

다른 원소와 비교만으로 정렬을 수행하는 **비교 정렬 알고리즘**

- n개의 데이터를 정렬할 때, 최악의 경우 O(n^2)번 비교를 수행하고, 평균적으로 O(nlogn)번의 비교를 수행
- 만약, 같은 값이 있는 경우 정렬 이후의 순서가 초기 순서와 달라질 수 있는 **불안정 정렬**에 속함
  > `5(1), 5(2), 3, 2, 1`을 정렬하면 `1, 2, 3, 5(2), 5(1)`이 됨

### 알고리즘

퀵 정렬은 분할 정복(divide and conquer) 방법을 통해 정렬함

1. 리스트 가운데서 하나의 원소를 고름(피벗)
2. 피벗 앞에는 피벗보다 값이 작은 원소들이 오고, 피벗 뒤에는 피벗보다 값이 큰 모든 원소들이 오도록 피벗을 기준으로 데이터를 둘로 나눔(분할)
3. 분할된 두 개의 작은 리스트에 대해 재귀(recursion)적으로 이 과정을 반복함. 재귀는 각 리스트의 크기가 0이나 1이 될 때까지 반복함

> 재귀 호출이 한 번 진행될 때 마다, 최소한 하나의 원소는 최종적으로 위치가 정해짐

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
