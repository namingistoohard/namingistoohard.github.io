---
layout: post
title:  "연결 리스트 Linked List"
---

> 이 글은 Udemy의 [Data Structures & Algorithms !](https://www.udemy.com/course/learn-data-structure-algorithms-with-java-interview/) 강의를 바탕으로 작성했습니다.

### 연결 리스트란?
선형 자료구조이고, 연결 리스트를 구성하는 각 요소(노드)는 각각 독립된 객체이다. 노드 객체는 최소 두 가지의 속성을 가진다.
* 값(value)
* 다음 노드를 가리키는 레퍼런스(next)

이로부터 알 수 있는 연결 리스트의 가장 큰 장점은, 크기가 가변적이라는 것이다.

연결 리스트의 구조를 그림으로 나타내면 대략 다음과 같다.

|haed|node|node|node|...|node|tail|

### 연결 리스트 vs. 배열

* separable object (linked list). 그러나 배열은 그 자체로 하나의 독립된 객체(오브젝트?)임. 그래서 배열의 셀은 따로 생기거나 삭제할 수 없음.
* variable size (linked list)
* random access (array). 연결리스트의 경우에는 무조건 처음부터 시작해서 차례로 접근해야 함. 그게 연결리스트의 가장 큰 단점 중 하나!

### 연결 리스트의 요소

* `node`: contains data & reference to next node.
  * 각 노드마다 다른 타입의 데이터를 저장할 수도 있음! 다른 타입으로 변경도 가능(한 듯)
* `head`: reference to first node in the list.
  * 첫 노드의 주소를 저장하고 있음.
  * 헤드가 필요한 이유? 이 링크드 리스트가 어디서 시작하는지, 즉 이게 어디 있는지 찾아야 해서
* `tail`: reference to last node of the list.
  * 마지막 노드의 위치를 저장함.
  * 뒤에 노드를 추가할 경우에 필요함!
  * 그래서 노드의 추가는 시간 복잡도가 O(1)임!

### 연결 리스트의 종류

* 1) 단일 연결 리스트 single linked list
  * in a singly linked list each node in the list stores the data of the node and a (physical) reference to the next node in the list. it does not store any reference to the previous node.
  * ![linked_list2](C:\Users\zoo2c\Desktop\ds_and_algo\linked_list2.PNG)
* 2) 원형 연결 리스트 circular linked list
  * in the case of a circular single linked list, the only change that occurs is that the end of the given list is linked back to the front.
  * ![linked_list3](C:\Users\zoo2c\Desktop\ds_and_algo\linked_list3.PNG)
  * last node가 첫 번째 노드의 주소를 가리킴
* 3) 이중 연결 리스트 double linked list
  * in double linked list each node contains two references, that references to the previous and next node.
  * ![linked_list4](C:\Users\zoo2c\Desktop\ds_and_algo\linked_list4.PNG)
  * (근데 내 질문: 그럼 각각의 노드는 메모리 상에서 연속적인가..? 꼭 그럴 필요는 없나? 아님 저 모든 정보들이 메모리 상의 저 한 지점 안에 들어 있는 건가..??)
  * 다른 방향으로 순회하는 게 좀 더 쉬움
* 4) 이중 원형 연결 리스트 circular double linked list
  * in the case of a circular doubly linked list, the only change that occurs is that the end of the given list is linked back to the front of the list and vice versa.
  * ![linked_list5](C:\Users\zoo2c\Desktop\ds_and_algo\linked_list5.PNG)

### why so many types of linked list

* single linked list
  * most basic form of linked list which give many flexibility to add/remove nodes at a runtime.
  * 그러나 보드게임하는 순서 이런 거에서 볼 수 있는, 마지막 차례가 끝나면 처음 차례로 돌아가는 이런 건 구현 x. 이건 환형 연결 리스트가 할 수 있음
* circular single linked list
  * when we want to loop through the list indefinitely until the list exists.
  * example: multiplayer board game. if we are tracking player's turn in linked list.
* double linked list
  * when we can move in both direction depending on requirement.
  * example: music player which has next and prev buttons.
* circular double linked list
  * when we want to loop through the list indefinitely until the list exists. we also want to move both foreward and backward.
  * example: "Alt + Tab" button in windows.
    * ![linked_list6](C:\Users\zoo2c\Desktop\ds_and_algo\linked_list6.PNG)

### how is linkedlist stored(represented) in memory(RAM)

* ![linked_list7](C:\Users\zoo2c\Desktop\ds_and_algo\linked_list7.PNG)
* 배열과 달리 메모리 상에서 연속적으로 배열(!)되어 있지 않음. 그래서 원소의 추가와 삭제가 자유롭고 아무 셀에나로의 자유로운 접근이 어려운 이유

### common operations of linked list

* 1) creation
* 2) insertion
* 3) traversal
* 4) searching for a certain value
* 5) deletion of a node
* 6) deletion of an entire linked list

### common operations of single linked list

#### creation of single linked list

* 일단 비어 있는 헤드와 테일을 만들고, 그 값을 null로 초기화한다. (아직 (가리킬) 노드가 없으므로)
* 비어 있는 노드를 만들고 레퍼런스를 null로 초기화하고 & data를 삽입한다.
* 이 노드와, 헤드와 테일 간의 링크를 만들어 준다. (헤드와 테일의 레퍼런스?를 이 노드의 주소값으로 채워 줌)

```
CreateSingleLinkedList(nodeValue):
  create a head, tail pointer and initialize with NULL // O(1)
  create a blank node // O(1)
  node.value = nodeValue; // O(1)
  node.next = null; // O(1)
  head = node; // O(1)
  tail = node; // O(1)
```

* 시간 복잡도: O(1)
* 공간 복잡도: O(1)
  * 헤드와 테일 포인터를 만들고, 빈 노드를 만드는 일 밖에 안 하니까

#### insertion in single linked list

* 1) when insert at start of LL

  * create a blank node
  * save a new value in it
  * link this node before the first node (save a reference of the first node. this automatically links the node.)
  * then head points the new node, not the previously first node. (update the address that head has, to the address of the new node)

* 2) when insert at end of LL

  * 첫 번째, 두 번째 과정은 동일함. 그 다음에 처음에 삽입하는 것과 다른 점은
    * 이전에 마지막 노드였던 노드의 레퍼런스를 NULL이 아니라 새로운 노드의 주소로 업데이트한다는 것
    * 그리고 tail을 새로운 노드에 연결하는 것

* 3) when insert at a specified location in LL

  * 역시 1, 2번째 과정은 동일함
  * 그 다음 첫 번째 노드부터 시작해서 새 노드의 바로 앞에 올 노드까지 차례로 순회해서 옴
  * 그 노드가 가지고 있는 reference variable을 새 노드의 reference variable로 복사해서 집어넣음 (이제 새 노드가 원래의 '다음 노드'를 가리켜야 하니까)
  * 새 노드가 들어갈 자리의 링크를 없앰 (즉, 새 노드의 앞에 올 노드의 reference variable을 새 노드의 주소로 업데이트함)

* 의사 코드

```
InsertInLinkedList(head, nodeValue, location):
  create a blank node // O(1)
  node.value = nodeValue; // O(1)
  if (!existsLinkedList(head)) // O(1)
    return error // Linked List does not exists // O(1)
  else if (location equals 0) // insert at first position // O(1)
    node.next = head; // head가 가리키는 게 곧 원래 첫 번째 노드의 주소니까 // O(1)
    head = node; // 이제 헤드는 새 노드의 주소를 가리키게 됨 // O(1)
  else if (location equals last) // insert at last position // O(1)
    node.next = null; // O(1)
    last.next = node // O(1)
    last = node // to keep track of last node // O(1)
  else // insert at specified position // O(1)
    loop: tmpNode = 0 to location-1 // loop till we reach specified node and end the loop // O(n)
    node.next = tmpNode.next // O(1)
    tmpNode.next = node // O(1)
```

* 시간 복잡도: O(n)
  * 최악의 경우 for문에서 끝에서 두번째 노드까지 갈 수 있음. O(n-1) = O(n)
* 공간 복잡도: O(1)
  * 참고로 O(1)이라는 것은 constant한 operation이라는 뜻임!

#### traversal of SLL

```
TraverseLinkedList(head):
  if head == NULL, then return // O(1)
  loop: head to tail // O(n)
    print currentNode.value // O(1)
```

* 시간 복잡도: O(n)
* 공간 복잡도: O(1)

#### search node in SLL

```
SearchNode(head, nodeValue):
  loop: tempNode = start to tail // O(n)
    if (tempNode.value equals nodeValue) // O(1)
      print tempNode.value // node value found // O(1)
      return // O(1)
  return // node value not found // O(1)
```

* ![linked_list8](C:\Users\zoo2c\Desktop\ds_and_algo\linked_list8.PNG)
* time complexity: O(n)
* space complexity: O(1)

#### deletion of node from SLL

* 1) delete first node

  * a) 이 노드가 LL의 유일한 노드일 경우, 헤드와 테일의 참조를 NULL로 바꾸면 이 노드가 더 이상 접근이 불가능해져서(이 노드를 참조하는 ?가 아무것도 없어서) 가비지 콜렉터가 수거(?)함
  * b) 그렇지 않을 경우, 헤드가 가리키는 주소를 두 번째 노드의 것으로 업데이트하면 됨. 그럼 또 GC가 수거해감

* 2) delete last node

  * a) 유일한 노드면: 1-a와 동일. 구조상으로는 차이가 없으나 우리가 실제로 코드를 짤 때 다루어야 할 상황들? 분기문? 이런 데서 차이가 있겠음
  * b) 그렇지 않으면: 일단 루프로 마지막에서 두 번째 노드까지 감. 그 노드의 next를 NULL로 업데이트. 그 다음에 테일이 이 노드를 대신 가리키게 함.

* 3) delete any node apart from above 2

  * 루프로 삭제하고 싶은 노드의 바로 앞 노드까지 감. 그 노드의 next가 삭제하고 싶은 노드의 다음 노드를 가리키게 함. 그럼 삭제하고 싶은 노드***를*** 가리키는 게 아무것도 없어서 GC가 수거함.

* 의사 코드

```
  DeleteNode(head, location):
    if (!existsLinkdeList(head)): // O(1)
      return error // Linkde List does not exists // O(1)
    else if (location equals 0): // we want to delete first node // O(1)
      head = head.next; // O(1)
      if this was the only element in list, than the update tail = null; // O(1)
    else if (location >= last): // O(1)
      if (current node is the only node in the list) then, head = tail = null; return; // O(1)
      loop till second last node (tmpNode) // O(n)
      tail = tmpNode; tmpNode.next = null; // O(1)
    else: // if any internal node needs to be deleted // O(1)
      loop: tmpNode = start to location-1 // we need to traverse toll we find the previous location // O(n)
      tmpNode.next = tmpNode.next.next // delete the required node // O(1)
  ```

* time complexity: O(n)
* space complexity: O(1)

#### delete entire SLL

* head와 tail의 참조만 제거하면 됨! 그럼 첫 번째 노드를 가리키는 게 아무것도 없어서 수거되고, 그럼 또 두 번째 노드를 가리키는 게 아무것도 없어서 두 번째 노드도 제고되고, ... 그렇게 순서대로 나머지 노드들에도 접근할 수 없게 됨. 마지막 노드를 참조하고 있는 tail도 꼭 null로 업데이트해 줘야 함

```
deleteLinkdeList(head, tail):
  head = null // O(1)
  tail = null // O(1)
```

* 시간복잡도: O(1)
* 공간복잡도: O(1)

#### time & space complexity of SLL

| particulars               | time complexity | space complexity |
| ------------------------- | --------------- | ---------------- |
| creation                  | O(1)            | O(1)             |
| insertion                 | O(n)            | O(1)             |
| searching                 | O(n)            | O(1)             |
| traversing                | O(n)            | O(1)             |
| deletion of a node        | O(n)            | O(1)             |
| deletion of a linked list | O(1)            | O(1)             |

### circular single linked list

#### creation

* 헤드와 테일을 만들고

* 빈 노드를 만ㄴ들고

* 값과 레퍼런스(NULL을 넣는 SLL과 달리, (지금 당장은 노드가 하나뿐이므로) 자기 자신의 주소를 넣음)를 넣고

* 헤드와 테일에 그 노드의 주소를 넣고

```
CreateSingleLinkedList(nodeValue):
  create a blank node // O(1)
  node.value = nodeValue; // O(1)
  node.next = node // O(1)
  head = node // O(1)
  tail = node // O(1)
```

* 시간복잡도: O(1)
* 공간복잡도: O(1)

#### insertion

* insert at start of linked list

  * 빈 노드를 만들어서 값과 레퍼런스(첫번째노드주소)를 넣고
  * 헤드의 주소를 새 노드의 것으로 바꾸고
  * 마지막 노드의 레퍼런스도 새 노드의 것으로 바꿈

* insert at end of linked list

  * 빈 노드를 만들어서 값을 넣고
  * 마지막 노드의 레퍼런스를 새 노드의 주소로 업데이트하고
  * 테일의 주소도 새 노드의 주소로 바꾸고
  * 새 노드의 레퍼런스를 첫 번째 노드의 주소로 바꿈 (이것만 SLL과 다른 점)

* insert at a specified location in linked list

  * (SLL과 같음)

```
InsertInLinkedList(head, nodeValue, location):
  create a blank node
  node.value = nodeValue;
  if (!existsLinkedList(head))
    return error // linked list does node exists
  else if (location equals 0)
    node.next = head;
    head = node;
    tail.next = node; // tail이 곧 원래의 마지막 노드이므로. SLL과 다른 점 1
  else if (location equals last) // insert at the last position
    node.next = head; // SLL과 다른 점 2
    tail.next = node
    tail = node // to keep track of the last node
  else
    loop: tmpNode = 0 to location-1 // loop til we reach specified node and end the loop. 여기만 O(n)이고 나머지 줄은 모두 O(1)
    node.next = tmpNode.next
    tmpNode.next = node
```

* 시간복잡도: O(n)

* 공간복잡도: O(1) // `tmpNode` 같은 임시 변수만 쓰기 때문에

#### traversing

* (SLL과 같음)

```
  TraverseLinkedList(head):
    if head == NULL, then return // O(1)
    loop: head to tail // O(n)
      print currentNode.value // O(1) (루프 때문에 n번 곱해짐)
  ```

* 시간복잡도: O(n)

* 공간복잡도: O(1)

#### searching

* SLL과 다 같지만 무한 루프를 막기 위해서, 매번 테일과 비교해야 함 (????? 이게 무슨 말이지? 알고리즘에는 이런 부분이 없는데... 저건 의사 코드라서 그런가)

```
SearchNode(head, nodeValue):
  loop: tmpNode = head to tail // O(n)
    if tmpNode.value equals nodeValue)
      print tmpNode.value
      return
  return // node value not found
```

* 시간복잡도: O(n)

* 공간복잡도: O(1)

#### deletion of a node

* delete first node

  * 헤드를 두 번째 노드의 주소로 업데이트하고
  * 마지막 노드도 두 번째 노드를 가리키도록 함
  * 다만 이 노드가 LL의 유일한 노드인 경우에는, 헤드와 테일만 NULL로 업데이트할 뿐만 아니라 삭제할 노드의 레퍼런스도 NULL로 업데이트해야 함! 유일한 노드는 자기 자신을 가리키고 있기 때문에. 삭제할 노드를 가리키는 것이 아무것도 없어야 함

* delete last node

  * 마지막에서 두 번째 노드까지 순회해 와서, 그 노드의 레퍼런스를 첫 번째 노드의 것으로 업데이트하고
  * 테일이 마지막에서 두 번째 노드를 가리키도록 업데이트함

* delete any node apart from above 2

  * 삭제할 노드의 직전 노드까지 순회해 와서 그것의 레퍼런스를 삭제할 노드의 다음 노드의 주소로 업데이트하면 됨

```
DeleteNode(head, location):
  if (!existsLinkedList(head)):
    return error
  else if (location equals 0) // delete first element
    head = head.next; tail.next = head
    if this was the only element in the list, then update head = tail = node.next = null;
  else if (location >= last):
    if (current node is the only node in the list) then, head = tail = node.next = null; return;
    loop till second last node (tmpNode)
    tail = tmpNode; tmpNode.next = head;
  else
    loop: tmpNode = start to location-1
    tmpNode.next = tmpNode.next.next // delete the required node
```

* 시간복잡도: O(n)

* 공간복잡도: O(1)

#### deletion of an entire CSLL

* ![linked_list9](C:\Users\zoo2c\Desktop\ds_and_algo\linked_list9.PNG)

* 링크 안의 어떤 노드도 외부에서 pointed되지 않도록 하면 됨

```
DeleteLinkedList(head, tail):
  head = NULL
  tail.next = NULL
  tail = NULL
```

* 시간복잡도: O(1)

* 공간복잡도: O(1) // 의사 코드가 아닌 실제 코드에서는 임시 변수를 몇 개 쓰게 될 것이기 때문에

#### time & space complexity of CSLL

| particulars                    | time complexity | space complexity |
| ------------------------------ | --------------- | ---------------- |
| creation                       | O(1)            | O(1)             |
| insertion                      | O(n)            | O(1)             |
| traversing                     | O(n)            | O(1)             |
| searching                      | O(n)            | O(1)             |
| deleting a node                | O(n)            | O(1)             |
| deleting an entire linked list | O(1)            | O(1)             |

### double linked list

* SLL과 달리 거꾸로도 갈 수 있음

  * ![linked_list10](C:\Users\zoo2c\Desktop\ds_and_algo\linked_list10.PNG)

#### creation

* 헤드와 테일 레퍼런스를 만들고,

* 빈 노드를 만들고,

* 이 노드에 값을 집어넣고, 이 노드가 현재로서는 유일한 노드이므로 prev와 next 레퍼런스 모두 NULL로 채움

* 헤드와 테일을 이 노드의 주소로 업데이트함

```
CreateDoubleLinkedList(nodeValue):
  create a blank node
  node.value = nodeValue;
  head = node;
  tail = node;
  node.next = node.prev = null; // prev를 제외하면 SLL과 동일함
```

* 시간복잡도: O(1)

* 공간복잡도: O(1)

#### insertion

* insert at start of linked list

  * 빈 노드를 만들어서 값을 넣고
  * 이 노드의 prev를 null로 채우고
  * 이 노드의 next를 원래의 첫 번째 노드의 주소로 채우고
  * 원래의 첫 번째 노드의 prev를 새 노드의 주소로 채우고
  * 헤드(의 레퍼런스)를 새 노드의 주소로 업데이트함

* insert at end of linked list

  * 빈 노드를 만들어서 값을 채우고
  * 이 노드의 next를 null로 채우고
  * 이 노드의 prev를 원래의 마지막 노드의 주소로 채우고
  * 원래의 마지막 노드의 next를 새 노드의 주소로 채우고
  * 테일의 레퍼런스를 새 노드의 주소로 업데이트함

* insert at any other place apart from above 2

  * 빈 노드를 만들어서 값을 채우고
  * 이 노드의 prev를, 새 노드의 이전 노드(가 될 노드)까지 순회해 와서 그 노드의 주소로 채우고, 이 이전 노드의 next를 새 노드의 주소로 채움
  * 그 다음에는 새 노드의 다음 노드(가 될 노드)까지 가서 새 노드의 next를 그 노드의 주소로 채우고, 그 노드의 prev를 새 노드의 주소로 채움

```
InsertNode(head, nodeValue, location):
  create a blank node
  node.value = nodeValue
  if (!existsLinkedList)
    return error
  else if (location equals 0) // insert at the first position
    node.next = head;
    node.prev = null;
    head.prev = node // 지금 여기서 head는 '이전의' 첫 번째 노드
    head = node
  else if (location equals last) // insert at the last position
    node.next = null;
    node.prev = tail;
    tail.next = node
    tail = node
  else // insert at specified location
    loop: tmpNode = 0 to location-1
    node.next = tmpNode.next;
    node.prev = tmpNode;
    tmpNode.next = node;
    node.next.prev = node;
```

* 시간복잡도: O(n)

* 공간복잡도: O(1)

#### traversal

* (SLL과 같음)

```
TraverseLinkedList(): // head를 인자로 넘겨 줘도 되고
  if head == NULL, then return
  loop: head to tail
    print currentNode.value
```

* 시간복잡도: O(n)

* 공간복잡도: O(1) // 루프 안에서의 임시 변수 때문에

#### reverse traversal

```
ReverseTraverseLinkedList(head):
  if head == NULL, then return // 연결리스트가 존재하는지 아닌지는 확인해야 하니까 (근데 테일로 확인해도 되지 않나..??)
  loop: tail to head
    print currentNode.value
```

* 시간복잡도: O(n)

* 공간복잡도: O(1)

#### searching

* (SLL과 같음)

```
SearchNode(head, nodeValue):
  loop: tmpNode = node to tail
    if (tmpNode.value equals nodeValue):
      print tmpNode.value
      return
  return // node value not found
```

* 시간복잡도: O(n)

* 공간복잡도: O(1)

#### deletion of a node

* delete first node

  * 일단 이 노드가 이 연결리스트의 유일한 노드인지 확인
  * 만약 그렇다면, 헤드와 테일을 null로 업데이트하면 됨 (이건 first와 last의 경우가 동일함)
  * 만약 그렇지 않다면, 헤드를 두 번쨰 노드의 주소로 업데이트하고, 두 번째 노드의 prev를 null로 업데이트하면 됨

* delete last node

  * 먼저 테일을 뒤에서 두 번째 노드의 주소로 업데이트하고, 뒤에서 두 번째 노드의 next를 null로 업데이트하면 됨

* delete any node apart from above 2

  * 삭제하고자 하는 노드의 직전 노드까지 간 다음, 이 직전 노드의 next를 삭제하고자 하는 노드의 다음 노드의 주소로 업데이트하고, 다음 노드의 prev는 이전 노드의 주소로 업데이트하면 됨

```
DeleteNode(head, location):
  if (!existsLinkedList):
    return error
    else if (location equals 0): // delete first element
      if this was the only element in the list, then update head = tail = null; return;
      head = head.next;
      head.prev = null;
    else if (location >= last):
      if this was the only element in the list, then update head = tail = null; return;
      tail = tail.prev;
      tail.next = null;
    else
      loop: tmpNode = start to location-1
      tmpNode.next = tmpNode.next.next // link current node with next node
      tmpNode.next.prev = tmpNode // link next node with current node
```

* 시간복잡도: O(n)

* 공간복잡도: O(1)

#### deletion of an entire DLL

* 헤드와 테일을 null로 업데이트한 다음에

* 각 노드들을 순회하면서 노드의 prev를 null로 업데이트해 줘야 함

```
DeleteLinkedList(head, tail):
  loop(tmp: head to tail):
    tmp.prev = null;
  head = tail = null;
```

* 시간복잡도: O(n)

* 공간복잡도: O(1)

#### time & space complexity of DLL

| particulars                       | time complexity | space complexity |
| --------------------------------- | --------------- | ---------------- |
| creation                          | O(1)            | O(1)             |
| insertion                         | O(n)            | O(1)             |
| traverse (both)                   | O(n)            | O(1)             |
| searching                         | O(n)            | O(1)             |
| deletion of a node                | O(n)            | O(1)             |
| deletion of an entire linked list | O(n)            | O(1)             |

### circular double linked list

* 마지막 노드의 next는 첫 번째 노드, 첫 번째 노드의 prev는 마지막 노드임

  * ![linked_list11](C:\Users\zoo2c\Desktop\ds_and_algo\linked_list11.PNG)

#### creation

* 먼저 빈 노드를 만들고, 값을 집어넣고,

* 헤드와 테일을 이 새 노드의 주소로 업데이트하고,

* 새 노드의 prev와 next를 ***자기 자신의 주소***로 채움

```
CreateCircularDoubleLinkedList(nodeValue):
  create a blank node
  node.value = nodeValue;
  head = node;
  tail = node;
  node.next = node.prev = node;
```

* 시간복잡도: O(1)

* 공간복잡도: O(1)

#### insertion

* insert at start of linked list

  * 빈 노드를 만들어서
  * 값을 채우고,
  * 이 노드의 next를 원래 첫 노드의 주소로 채우고,
  * 이 노드의 prev를 마지막 노드의 주소로 채우고,
  * 마지막 노드의 next를 새 노드의 주소로 업데이트하고,
  * 원래 첫 번째 노드의 prev를 새 노드의 주소로 업데이트하고,
  * 헤드를 새 노드의 주소로 업데이트함

* insert at end of linked list

  * 빈 노드를 만들어서
  * 값을 채우고,
  * 이 노드의 next를 첫 번째 노드의 주소로 채우고,
  * 이 노드의 prev를 원래 마지막 노드의 주소로 채우고,
  * 원래 마지막 노드의 next를 새 노드의 주소로 업데이트하고,
  * 첫 노드의 prev를 새 노드의 주소로 업데이트하고,
  * 테일을 새 노드의 주소로 업데이트함

* insert at any other place apart from above 2

  * 빈 노드를 만들어서
  * 값을 채우고,
  * 이 노드의 앞 노드가 될 노드까지 순회해 와서 그것의 주소가 새 노드의 prev가 되고,
  * 이 노드의 뒤 노드의 주소가 새 노드의 next가 되고,
  * 앞 노드의 next는 새 노드의 주소가 되고,
  * 뒤 노드의 prev도 새 노드의 주소가 됨

```
InsertNode(head, nodeValue, location):
  create a blank node
  node.value = nodeValue;
  if (!existsLinkedList(head)):
    return error
    else if (location equals 0):
      node.next = head;
      node.prev = tail;
      head.prev = node;
      head = node;
      tail.next = node;
    else if (location equals last):
      node.next = head;
      node.prev = tail;
      head.prev = node;
      tail.next = node;
      tail = node;
    else:
      loop tmpNode = 0 to location-1
      node.next = tmpNode.next;
      node.prev = tmpNode;
      tmpNode.next = node;
      node.next.prev = node;
```

* 시간복잡도: O(n)

* 공간복잡도: O(1)

#### traversal

* *실제 코드에서는!!!!* 매번 이번 노드가 테일인지 아닌지 (즉 이 노드가 마지막 노드고 따라서 루프를 종료해야 하는지) 체크해야 함

```
TraverseLinkedList():
  if head == null, then return
  loop: head to tail
    print currentNode.value
```

* 시간복잡도: O(n)

* 공간복잡도: O(1)

#### reverse traversal

* 이 때도 매번 테일인지 체크해서 무한 루프를 방지해야 함

```
ReverseTraversalLinkedList():
  if head == null, then return
  loop: tail to head
    print currentNode.value
```

* 시간복잡도: O(n)

* 공간복잡도: O(1)

#### searching

* 이 때도 매번 테일인지 체크해서 무한 루프를 방지해야 함

```
SearchNode(nodeValue):
  loop: tmpNode = head to tail
    if (tmpNode.value equals nodeValue)
      print tmpNode.value
      return
  return
```

* 시간복잡도: O(n)

* 공간복잡도: O(1)

#### deletion of a node (삭제하고 싶은 노드를 가리키는 모든 연결을 끊는 일!)

* delete first node

  * 일단 마지막 노드의 next를 두 번째 노드의 주소로 업데이트함
  * 헤드도 두 번째 노드의 주소로 업데이트함
  * 두 번째 노드의 prev를 마지막 노드의 주소로 업데이트함
  * 만약 첫 번째 노드가 유일한 노드라면, 헤드, 노드, 그리고 자기 자신의 prev와 next를 null로 업데이트해 주면 됨 (유일한 노드가 마지막 노드..! 인 경우에도 동일함)

* delete last node

  * 먼저 테일을 뒤에서 두 번째 노드의 주소로 업데이트함
  * 뒤에서 두 번째 노드의 next를 첫 번째 노드의 주소로 업데이트함
  * 첫 번째 노드의 prev를 뒤에서 두 번째 노드의 주소로 업데이트함

* delete any other node apart from above 2

  * 삭제하고 싶은 노드의 직전 노드까지 가서
  * 이 직전 노드의 next를 삭제하고 싶은 노드의 다음 노드의 주소로 업데이트하고
  * 삭제하고 싶은 노드의 다음 노드의 prev를 위에서 언급한 '직전 노드'의 주소로 업데이트하면 됨

```
DeleteNode(head, location):
  if (!existsLinkedLise(head)):
    return error
    else if (location equals 0):
      if this was the only element in the list, then update head.next = head.prev = head = tail = null; return;
      head = head.next;
      head.prev = tail;
      tail.next = head;
    else if (location >= last):
      if this was the only element in the list, then update head.next = head.prev = head = tail = null; return;
      tail = tail.prev;
      tail.next = head;
      head.prev = tail;
    else:
      loop: tmpNode = start to location-1
      tmpNode.next = tmpNode.next.next
      tmpNode.next.prev = tmpNode
```

* 시간복잡도: O(n)

* 공간복잡도: O(1)

#### deletion of an entire CDLL

* 마지막 노드의 next를 null로

* 그 다음 첫 번째 노드의 prev를 null로, ...모든 노드의 prev를 null로

* 마지막으로 헤드와 테일을 null로

```
DeleteLinkedList(head, tail):
  tail.next = null;
  loop(tmp: head to tail)
    tmp.prev = null;
  head = tail = null
```

* 시간복잡도: O(n)

* 공간복잡도: O(1)

#### time & space complexity of CDLL

| particulars                       | time complexity | space complexity |
| --------------------------------- | --------------- | ---------------- |
| creation                          | O(1)            | O(1)             |
| insertion                         | O(n)            | O(1)             |
| traversing (both)                 | O(n)            | O(1)             |
| searching                         | O(n)            | O(1)             |
| deletion of a node                | O(n)            | O(1)             |
| deletion of an entire linked list | O(n)            | O(1)             |

* 무슨 리스트 길이..? 이런 걸 쓰면 O(logn) 이런 말을 했는데 못 알아들었다

### SLL vs CSLl vs DLL vs CDLL

시간 복잡도 비교 표
| particulars                       | array         | linked list     |
| --------------------------------- | ------------- | --------------- |
| create                            | O(1)          | O(1)            |
| insertion at first position       | O(1)          | O(1)            |
| insertion at last position        | O(1)          | O(1)            |
| insertion at Kth position         | O(1)          | O(n)            |
| deletion from first position      | O(1)          | O(1)            |
| deletion form last position       | O(1)          | **O(n)/O(1)**^1 |
| deletion from Kth position        | O(1)          | O(n)            |
| searching in unsorted data        | O(n)          | O(n)            |
| searching in sorted data          | **O(logn)**^2 | O(n)            |
| accessing Nth element             | O(1)          | O(n)            |
| traverse                          | O(n)          | O(n)            |
| deleting entire array/linked list | O(1)          | **O(n)/O(1)**^3 |

* ^1) 이중 연결 리스트의 경우에는 O(1)

* ^2) 바이너리 서치를 이용할 경우

* ^3) 이중 연결 리스트의 경우에는 O(n)

### practical uses of linked list

* "Alt-Tab" button: 이중 원형 연결 리스트
* Windows photo viewer: 이중 원형 연결 리스트
