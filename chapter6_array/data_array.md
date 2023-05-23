### 0. Introduction

정렬 알고리즘
- 데이터를 특정 기준에 따라 순서대로 나열하는 것
- 일반적으로 문제 상황에 따라 적절한 정렬 알고리즘이 공식처럼 사용되므로, 다양한 문제를 풀어보며 유형을 익힐 필요가 있음

### 1. 선택 정렬 (Selection Sort)

선택 정렬
- 처리되지 않은 데이터 중 가장 작은 데이터를 선택하여 맨 앞에 있는 데이터와 바꾸는 과정을 반복
- 매번 현재 범위에서 가장 작은 데이터를 골라 제일 앞쪽으로 보내는 것

```
array = [7, 5, 9, 0, 3, 1, 6, 2, 4, 8]

for i in range(len(array)):
    min_index = i # 가장 작은 원소의 idx
    for j in range(i + 1, len(array)):
        if array[min_index] > array[j]:
            min_index = j
    array[i], array[min_index] = array[min_index], array[i] # swap
   
print(array)
```

### 2. 삽입 정렬 (Insertion Sort)

삽입 정렬
- 처리되지 않은 데이터를 하나씩 골라서 적절한 위치에 삽입하면서 수행
- 데이터를 하나씩 확인하면서 어느 위치에 들어가는 것이 맞는지 계산하여, 적절한 위치에 들어가도록 정렬해주는 것

```
array = [7, 5, 9, 0, 3, 1, 6, 2, 4, 8]

for i in range(1, len(array)): # 두 번째 원소부터 삽입됨
    for j in range(i, 0, -1): # index i부터 1까지 1씩 감소하며 반복함
        if array[j] < array[j - 1]: # 한 칸씩 왼쪽으로 이동하며 비교
            array[j], array[j - 1] = array[j - 1], array[j]
        else: # 자신보다 작은 데이터를 만나면 그 위치에서 멈춤
            break
            
print(array)
```

### 3. 퀵 정렬 (Quick Sort)

퀵 정렬
- 빠른 정렬 알고리즘 중 하나
- 일반적인 데이터 특성과 상관 없이 표준적으로 사용할 수 있는 정렬 알고리즘 중 하나로 볼 수 있음
- 기준 데이터를 설정하고, 그 데이터보다 큰 데이터와 작은 데이터의 위치를 바꾸면서 동작

```
array = [5, 7, 9, 0, 3, 1, 6, 2, 4, 8]

def quick_sort(array, start, end):
    if start >= end: # (분할된 데이터 묶음의) 원소가 1개인 경우 종료
        return
    pivot = start # 피벗을 첫 번째 원소로 설정
    right = end
    while(left <= right):
        # 피벗보다 큰 데이터를 찾을 때까지 오른쪽으로 가면서
        while(left <= end and array[left] <= array[pivot]):
            left += 1
        # 피벗보다 작은 데이터를 찾을 때까지 왼쪽으로 가면서
        while(right > start and array[right] >= array[pivot]):
            right -= 1
        if(left > right): # 엇갈린 경우 피벗과 작은 데이터 swap
            array[right], array[pivot] = array[pivot], array[right]
        else: # 엇갈리지 않은 경우 작은 데이터와 큰 데이터 swap
            array[left], array[right] = array[right], array[left]
    # 분할 이후 왼쪽 부분과 오른쪽 부분에서 각각 정렬 수행
    quick_sort(array, start, right - 1)
    quick_sort(array, right + 1, end)

quick_sort(array, 0, len(array) - 1)
print(array)
```

### 4. 계수 정렬 (Counting Sort)

계수 정렬
- 특정 조건이 부합할 때만 사용할 수 있지만, 매우 빠르게 동작하는 정렬 알고리즘
- 특정 조건은 바로 데이터의 크기 범위가 제한되어 정수 형태로 표현할 수 있을 때 사용 가능하다는 것

```
# 모든 원소의 값이 0보다 크거나 같다고 가정
array = [7, 5, 9, 0, 3, 1, 6, 2, 9, 1, 4, 8, 0, 5, 2]
# 모든 범위를 포함하는 리스트 선언(모든 값은 0으로 초기화)
count = [0] * (max(array) + 1) # 위 예시에서 0 ~ 9까지 10개

for i in range(len(array)):
    count[array[i]] += 1 # 각 데이터에 해당하는 인덱스 값 증가

for i in range(len(count)): # 리스트에 기록된 정렬 정보 확인
    for j in range(count[i])):
        print(i, end=' ') # 띄어쓰기를 구분으로 등장한 횟수만큼 인덱스 출력
```
