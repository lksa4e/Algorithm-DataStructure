## 링크드 리스트 (Linked List)

### 1. 링크드 리스트 (Linked List) 구조
* 연결 리스트라고도 함
* 배열은 순차적으로 연결된 공간에 데이터를 나열하는 데이터 구조
* 링크드 리스트는 떨어진 곳에 존재하는 데이터를 화살표로 연결해서 관리하는 데이터 구조
* <font color='#BF360C'>본래 C언어에서는 주요한 데이터 구조이지만, 파이썬은 리스트 타입이 링크드 리스트의 기능을 모두 지원</font>

* 링크드 리스트 기본 구조와 용어
  - 노드(Node): 데이터 저장 단위 (데이터값, 포인터) 로 구성
  - 포인터(pointer): 각 노드 안에서, 다음이나 이전의 노드와의 연결 정보를 가지고 있는 공간

<br>
* 일반적인 링크드 리스트 형태
<img src="https://www.fun-coding.org/00_Images/linkedlist.png" />
(출처: wikipedia, https://en.wikipedia.org/wiki/Linked_list)

* 더블 링크드 리스트(Doubly linked list)
  - 이중 연결 리스트라고도 함
  - 장점: 양방향으로 연결되어 있어서 노드 탐색이 양쪽으로 모두 가능
  <br>
<img src="https://www.fun-coding.org/00_Images/doublelinkedlist.png" />
(출처: wikipedia, https://en.wikipedia.org/wiki/Linked_list)

### 2. 링크드 리스트의 장단점 (전통 C언어에서의 배열과 링크드 리스트)
* 장점
  - 미리 데이터 공간을 미리 할당하지 않아도 됨
    - 배열은 **미리 데이터 공간을 할당** 해야 함
* 단점
  - 연결을 위한 별도 데이터 공간이 필요하므로, 저장공간 효율이 높지 않음
  - 연결 정보를 찾는 시간이 필요하므로 접근 속도가 느림
  - 중간 데이터 삭제시, 앞뒤 데이터의 연결을 재구성해야 하는 부가적인 작업 필요

### 3. 링크드 리스트 주의점
* 추가/삭제하는 경우 기존 앞 노드와 뒤 노드의 연결관계, head/tail를 갱신해주어야 함
    - 맨 앞에 추가/삭제하는 경우 -> head 변경
    - 맨 뒤에 추가/삭제하는 경우 -> tail 변경

```python
#구현

class Node:
    def __init__(self, data, prev = None, next = None):
        self.prev = prev
        self.next = next
        self.data = data
        
class list_mgmt:
    def __init__(self, data):
        self.head = Node(data)
        self.tail = self.head
    
    def add(self,data): # 오름차순 정렬 링크드리스트 만들기
        if self.head == None:
            self.head = Node(data)
            self.tail = self.head
        else:
            node = self.head
            if node.data > data:
                node.prev = Node(data,None,node)
                self.head = node.prev
                return
            while node.next:
                if node.data > data:
                    New = Node(data,node.prev,node)
                    node.prev.next = New
                    node.prev = New
                    return
                else:
                    node = node.next
            if node.data > data:
                New = Node(data,node.prev,node)
                node.prev.next = New
                node.prev = New
                return
            else:
                New = Node(data,node)
                node.next = New
                self.tail = New
    def remove(self,data):
        if self.head == None:
            print(f"there are no data {data} in linked_list")
        else:
            node = self.head
            if node.data == data:
                node.next.prev = None
                self.head = node.next
                del node
                return
            while node.next:
                if node.data == data:
                    node.prev.next = node.next
                    node.next.prev = node.prev
                    del node
                    return
                else:
                    node = node.next
            print(f"there are no data {data} in linked_list")
    def desc(self):
        if self.head == None:
            print("there are no data in linked_list")
        else:
            node = self.head
            while node.next:
                print(node.data)
                node = node.next
            print(node.data)
