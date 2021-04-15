정렬(Sort)
============

## 1. 버블 정렬 (bubble sort)
* 두 인접한 데이터를 비교해서, 앞에 있는 데이터가 뒤에 있는 데이터보다 크면, 자리를 바꾸는 정렬 알고리즘

<img src="https://upload.wikimedia.org/wikipedia/commons/c/c8/Bubble-sort-example-300px.gif" width=400/>
> 출처: https://en.wikipedia.org/wiki/Bubble_sort

### 1.1. 알고리즘 구현
  - n개의 리스트가 있는 경우 최대 n-1번의 로직을 적용한다.
  - 로직을 1번 적용할 때마다 가장 큰 숫자가 뒤에서부터 1개씩 결정된다.
  - 로직이 경우에 따라 일찍 끝날 수도 있다. 따라서 로직을 적용할 때 한 번도 데이터가 교환된 적이 없다면 이미 정렬된 상태이므로 더 이상 로직을 반복 적용할 필요가 없다.
  <img src="https://www.fun-coding.org/00_Images/bubblealgo.png" />

```
1. for num in range(len(data_list)) 반복
2. swap = 0 (교환이 되었는지를 확인하는 변수를 두자)
2. 반복문 안에서, for index in range(len(data_list) - num - 1) n - 1번 반복해야 하므로
3. 반복문안의 반복문 안에서, if data_list[index] > data_list[index + 1] 이면
4.    data_list[index], data_list[index + 1] = data_list[index + 1], data_list[index]
5.    swap += 1
6. 반복문 안에서, if swap == 0 이면, break 끝
```

### 1.2. 알고리즘 분석
* 반복문이 두 개 O($n^2$)
  - 최악의 경우, <font size=5em>$\frac { n * (n - 1)}{ 2 }$</font>
* 완전 정렬이 되어 있는 상태라면 최선은 O(n)

### 1.3. 구현
```python
def bubblesort(data):
    for index in range(len(data) - 1):
        swap = False
        for index2 in range(len(data) - index - 1):
            if data[index2] > data[index2 + 1]:
                data[index2], data[index2 + 1] = data[index2 + 1], data[index2]
                swap = True
        
        if swap == False:
            break
    return data
```

## 2. 선택 정렬(Selection Sort)
* 다음과 같은 순서를 반복하며 정렬하는 알고리즘
  1. 주어진 데이터 중, 최소값을 찾음
  2. 해당 최소값을 데이터 맨 앞에 위치한 값과 교체함
  3. 맨 앞의 위치를 뺀 나머지 데이터를 동일한 방법으로 반복함

<img src="https://upload.wikimedia.org/wikipedia/commons/9/94/Selection-Sort-Animation.gif" width=100>

출처: https://en.wikipedia.org/wiki/Selection_sort

### 2.1. 알고리즘 구현
```
1. for stand in range(len(data_list) - 1) 로 반복
2. lowest = stand 로 놓고,
3. for num in range(stand, len(data_list)) stand 이후부터 반복
   - 내부 반복문 안에서 data_list[lowest] > data_list[num] 이면, 
     - lowest = num
4. data_list[num], data_list[lowest] = data_list[lowest], data_list[num]   
```

### 2.2. 알고리즘 분석
* 반복문이 두 개 O($n^2$)
  - 실제로 상세하게 계산하면, <font size=5em>$\frac { n * (n - 1)}{ 2 }$</font>

### 2.3. 구현
```python
def selection_sort(data):
    for stand in range(len(data) - 1):
        lowest = stand
        for index in range(stand + 1, len(data)):
            if data[lowest] > data[index]:
                lowest = index
        data[lowest], data[stand] = data[stand], data[lowest]
    return data
```

## 3. 삽입 정렬(Insertion Sort)
* 삽입 정렬은 두 번째 인덱스부터 시작
* 해당 인덱스(key 값) 앞에 있는 데이터(B)부터 비교해서 key 값이 더 작으면, B값을 뒤 인덱스로 복사
* 이를 key 값이 더 큰 데이터를 만날때까지 반복, 그리고 큰 데이터를 만난 위치 바로 뒤에 key 값을 이동

<img src="https://upload.wikimedia.org/wikipedia/commons/9/9c/Insertion-sort-example.gif" />

> 출처: https://commons.wikimedia.org/wiki/File:Insertion-sort-example.gif

### 3.1. 알고리즘 구현
```
1. for stand in range(len(data_list)) 로 반복
2. key = data_list[stand]
3. for num in range(stand, 0, -1) 반복
   - 내부 반복문 안에서 data_list[stand] < data_list[num - 1] 이면, 
     - data_list[num - 1], data_list[num] = data_list[num], data_list[num - 1]   
```

### 3.2. 알고리즘 분석
* 반복문이 두 개 O($n^2$)
  - 최악의 경우, <font size=5em>$\frac { n * (n - 1)}{ 2 }$</font>
* 완전 정렬이 되어 있는 상태라면 최선은 O(n)

### 3.3. 구현
```python
def insertion_sort(data):
    for index in range(len(data) - 1):
        for index2 in range(index + 1, 0, -1):
            if data[index2] < data[index2 - 1]:
                data[index2], data[index2 - 1] = data[index2 - 1], data[index2]
            else:
                break
    return data
```

## 4. 병합 정렬 (merge sort) 
* 재귀용법을 활용한 정렬 알고리즘
  1. 리스트를 절반으로 잘라 비슷한 크기의 두 부분 리스트로 나눈다.
  2. 각 부분 리스트를 재귀적으로 합병 정렬을 이용해 정렬한다.
  3. 두 부분 리스트를 다시 하나의 정렬된 리스트로 합병한다.


<img src="https://upload.wikimedia.org/wikipedia/commons/c/cc/Merge-sort-example-300px.gif" width=500/>

출처: [위키피디아](https://ko.wikipedia.org/wiki/%ED%95%A9%EB%B3%91_%EC%A0%95%EB%A0%AC)

### 4.1. 알고리즘 구현
* mergesplit 함수 만들기
  - 만약 리스트 갯수가 한개이면 해당 값 리턴
  - 그렇지 않으면, 리스트를 앞뒤, 두 개로 나누기
  - left = mergesplit(앞)
  - right = mergesplit(뒤)
  - merge(left, right)

* merge 함수 만들기
  - 리스트 변수 하나 만들기 (sorted)
  - left_index, right_index = 0
  - while left_index < len(left) or right_index < len(right):
    - 만약 left_index 나 right_index 가 이미 left 또는 right 리스트를 다 순회했다면, 그 반대쪽 데이터를 그대로 넣고, 해당 인덱스 1 증가
    - if left[left_index] < right[right_index]:
      - sorted.append(left[left_index])
      - left_index += 1
    - else:
      - sorted.append(right[right_index])
      - right_index += 1

### 4.2. 알고리즘 분석
  - 다음을 보고 이해해보자
    - 몇 단계 깊이까지 만들어지는지를 depth 라고 하고 i로 놓자. 맨 위 단계는 0으로 놓자.
      - 다음 그림에서 n/$2^2$ 는 2단계 깊이라고 해보자.
      - 각 단계에 있는 하나의 노드 안의 리스트 길이는 n/$2^2$ 가 된다.
      - 각 단계에는 $2^i$ 개의 노드가 있다.
    - 따라서, 각 단계는 항상 <font size=4em>$2^i * \frac { n }{ 2^i } = O(n)$</font>
    - 단계는 항상 $log_2 n$ 개 만큼 만들어짐, 시간 복잡도는 결국 O(log n), 2는 역시 상수이므로 삭제
    - 따라서, 단계별 시간 복잡도 O(n) * O(log n) = O(n log n)

<img src="https://www.fun-coding.org/00_Images/mergesortcomplexity.png" />


### 4.3. 구현
```python
def merge(left, right):
    merged = list()
    left_point, right_point = 0, 0
    
    # case1 - left/right 둘다 있을때
    while len(left) > left_point and len(right) > right_point:
        if left[left_point] > right[right_point]:
            merged.append(right[right_point])
            right_point += 1
        else:
            merged.append(left[left_point])
            left_point += 1

    # case2 - left 데이터가 없을 때
    while len(left) > left_point:
        merged.append(left[left_point])
        left_point += 1
        
    # case3 - right 데이터가 없을 때
    while len(right) > right_point:
        merged.append(right[right_point])
        right_point += 1
    
    return merged


def mergesplit(data):
    if len(data) <= 1:
        return data
    medium = int(len(data) / 2)
    left = mergesplit(data[:medium])
    right = mergesplit(data[medium:])
    return merge(left, right)
```

## 5. 퀵 정렬 (quick sort) 
* 기준점(pivot 이라고 부름)을 정해서, 기준점보다 작은 데이터는 왼쪽(left), 큰 데이터는 오른쪽(right) 으로 모으는 함수를 작성함
* 각 왼쪽(left), 오른쪽(right)은 재귀용법을 사용해서 다시 동일 함수를 호출하여 위 작업을 반복함
* 함수는 왼쪽(left) + 기준점(pivot) + 오른쪽(right) 을 리턴함

### 5.1. 알고리즘 구현
* quicksort 함수 만들기
  - 만약 리스트 갯수가 한개이면 해당 리스트 리턴
  - 그렇지 않으면, 리스트 맨 앞의 데이터를 기준점(pivot)으로 놓기
  - left, right 리스트 변수를 만들고,
  - 맨 앞의 데이터를 뺀 나머지 데이터를 기준점과 비교(pivot)
    - 기준점보다 작으면 left.append(해당 데이터)
    - 기준점보다 크면 right.append(해당 데이터)
  - return quicksort(left) + pivot + quicksort(right) 로 재귀 호출
  
> 리스트로 만들어서 리턴하기: return quick_sort(left) + [pivot] + quick_sort(right)
 
### 5.2. 알고리즘 분석
* <font color='#BF360C'>병합정렬과 유사, 시간복잡도는 O(n log n)</font>
  - 단, 최악의 경우 
    - 맨 처음 pivot이 가장 크거나, 가장 작으면
    - 모든 데이터를 비교하는 상황이 나옴
    - O($n^2$)
<img src="https://www.fun-coding.org/00_Images/quicksortworks.jpg" />

### 5.3. 구현
```python
def qsort(data):
    if len(data) <= 1:
        return data
    
    pivot = data[0]

    left = [ item for item in data[1:] if pivot > item ]
    right = [ item for item in data[1:] if pivot <= item ]
    
    return qsort(left) + [pivot] + qsort(right)
```
