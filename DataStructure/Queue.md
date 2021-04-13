##  큐 (Queue)

### 1. 큐 구조

  - FIFO(First-In, First-Out) 또는 LILO(Last-In, Last-Out) 방식으로 스택과 꺼내는 순서가 반대
 <img src="https://www.fun-coding.org/00_Images/queue.png" />
* 출처: http://www.stoimen.com/blog/2012/06/05/computer-algorithms-stack-and-queue-data-structure/

  - Enqueue: 큐에 데이터를 넣는 기능
  - Dequeue: 큐에서 데이터를 꺼내는 기능

### 2. Python queue 라이브러리 -- import queue
**queue 라이브러리 - Queue(), LifoQueue(), PriorityQueue() 제공**
  - Queue(): 가장 일반적인 큐 자료 구조
  - LifoQueue(): 나중에 입력된 데이터가 먼저 출력되는 구조 <stack>
  - PriorityQueue(): 우선순위가 높은 순으로 데이터 출력

### 3. 큐 사용처
- 멀티 태스킹을 위한 프로세스 스케쥴링 방식을 구현하기 위해 많이 사용됨 (운영체제 참조)

> 큐의 경우에는 장단점 보다는 (특별히 언급되는 장단점이 없음), 큐의 활용 예로 프로세스 스케쥴링 방식을 함께 이해해두는 것이 좋음

```python

import queue
data_queue = queue.Queue()  # queue 선언
data_queue = queue.LifoQueue()
data_queue = queue.PriorityQueue()
data_queue.put(1)
data_queue.qsize()
data_queue.get()

data_queue.put((5, 1)) #PriorityQueue push

# queue 구현
queue_list = list()
def enqueue(data):
    queue_list.append(data)
    
def dequeue(i):
    data = queue_list[i]
    del queue_list[i]
    return data
