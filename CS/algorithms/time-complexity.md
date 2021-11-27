### Time Complexity

문제를 해결하려는데 걸리는 시간과 입력의 함수 관계

- 주로 빅-오 표기법을 사용하여 나타냄

### 빅-오 표기법

- 계수와 낮은 차수의 항을 제외시키는 방법
- 점근적으로 묘사한다고 표현할 수 있음
- 예를 들어, `5n^3+3n`의 시간복잡도는 `O(n^3)`

### 시간 복잡도 설명

|      이름      | 시간복잡도 | 수행 횟수 예시 |           알고리즘 예시           |
| :------------: | :--------: | :------------: | :-------------------------------: |
|   상수 시간    |    O(1)    |       10       | 정수가 짝숭이거나 홀수이거나 결정 |
|   로그 시간    |  O(logn)   | logn, log(n^2) |             이진탐색              |
|   선형 시간    |    O(n)    |       n        |     배열에서 가장 큰 수 탐색      |
| 선형 로그 시간 |  O(nlogn)  |     nlogn      |        가장 빠른 비교 정렬        |
|   지수 시간    |   2^O(n)   |      10^n      |            동적 계획법            |

### 정렬 알고리즘 시간복잡도 정리

|   Algorithm    | Space Complexity | (average) Time Complexity | (worst) Time Complexity |
| :------------: | :--------------: | :-----------------------: | :---------------------: |
|  Bubble sort   |       O(1)       |          O(n^2)           |         O(n^2)          |
| Selection sort |       O(1)       |          O(n^2)           |         O(n^2)          |
| Insertion sort |       O(1)       |          O(n^2)           |         O(n^2)          |
|   Merge sort   |       O(n)       |         O(nlogn)          |        O(nlogn)         |
|   Heap sort    |       O(1)       |         O(nlogn)          |        O(nlogn)         |
|   Quick sort   |       O(1)       |         O(nlogn)          |         O(n^2)          |
|   Count sort   |       O(n)       |           O(n)            |          O(n)           |
|   Radix sort   |       O(n)       |           O(n)            |          O(n)           |
