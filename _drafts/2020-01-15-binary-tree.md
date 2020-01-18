---
layout: post
title:  "이진 트리 Binary Tree"
---

* What is Tree

  * ex) properties of decision tree (which cooling device should I buy)
    * used to represent data in hierarchical form (lower => more specialized)
    * every node has 2 components (Data & References to its sub-category)
    * at top it has Base product and 2 'products' called Left sub-category and Right sub-category under it.
  * => properties of Tree
    * used to represent data in hierarchical form
    * every node (ideally) has 2 components (Data & Reference)
    * it has a Root node and 2 disjoint binary tree called Left subtree and Right subtree.

* Why learn Tree

  * 배열이나 연결리스트보다 효율적인 면이 있음
  * 연결리스트의 경우 각종 오퍼레이션 시간복잡도가 O(n)인데 트리의 경우 O(logn)으로 줄일 수 있다고

* Tree Terminologies

  * Root: Node with no parent
  * Edge: Link from Parent to Child
  * Leaf: Node with no children
  * Sibling: Children of same parent
  * Ancestor: means Parent, grand-Parent, great grand parent, and so on for a given node.
  * Depth of node: Length of the path from root to node.
  * Height of node: Length of the path from that node to the deepest node (해당 노드의 자식 노드들 중에!).
  * Height of tree: Same as height of Root node
  * Depth of tree: Same as depth of Root node (= 0)
  * Predecessor(전임자, 선배, (조상)): Predecessor of a node is the immediate previous node in In-order(Inorder) traversal of the Binary Tree.
    * inorder traversal(한국어 명칭 찾아 두기!!): 왼쪽 서브트리 -> 루트 -> 오른쪽 서브트리 순으로 순회
      * ![binary_tree](C:\Users\zoo2c\Desktop\ds_and_algo\binary_tree.PNG)
    * 위의 그림을 바탕으로 했을 때 100 노드의 predecessor는 90 노드임
  * Successor(후계자, 상속인): Successor of a node is the immediate next node in Inorder traversal of the Binary Tree.

* What & Why of Binary Tree

  * What is Binary Tree
    * a tree is called as binary tree if each node has zero, one or two child.
    * it is a family of Data Structure (BST, Heap tree, AVL, Red-Black, Syntax Tree, Huffman Coding Tree, etc.) <- 이 모든 트리들이 이진 트리의 일종임
  * Why should we learn Binary Tree?
    * Prerequisite for more advanced trees (BST, AVL, Red-Black, Expression Tree, etc...)
    * Binary Tree is used in solving specific problems like:
      * Huffman Coding
      * Heap (Priority Queue)
      * Expression parsing

* Types of Binary Tree

  * Strict Binary Tree(정 이진트리): if each node has either 2 children or none.
    * 아니 뭐지 이거를 full binary tree라고 부르는 데도 있네....??!!
    * ==> full binary tree가 맞다?
  * Full Binary Tree(포화이진트리): if each non-leaf node has 2 children and all leaf nodes are at same level
    * 아니 이거를 perfect binary tree라고도 하나 보네
    * ==> perfect binary tree가 맞다?
  * Complete Binary Tree(완전이진트리): if all levels are completely filled except possibly the last level and the last level has all keys as left as possible.
  * ![binary_tree2](C:\Users\zoo2c\Desktop\ds_and_algo\binary_tree2.PNG)

* How is Tree Represented in Code

  * suppose that we should implement this tree structure.
    * ![binary_tree5](C:\Users\zoo2c\Desktop\ds_and_algo\binary_tree5.PNG)
  * Using Linked List
    * ![binary_tree3](C:\Users\zoo2c\Desktop\ds_and_algo\binary_tree3.PNG)
  * Using Array
    * ![binary_tree4](C:\Users\zoo2c\Desktop\ds_and_algo\binary_tree4.PNG)
    * never use 0th cell, and first(root) node value is stored at 1st cell.
    * left child - cell[2x] // x == cell number of a parent node
    * right child - cell[2x+1]

* Binary Tree (Linked List)

  * Create blank Binary Tree

    * ```
      createBinaryTree()
      	Create an object of Binary Tree class
      ```

    * 시간복잡도: O(1)

    * 공간복잡도: O(1)

  * 참고로 앞으로 나올 모든 순회에 예시로 쓰일 트리

    * ![binary_tree6](C:\Users\zoo2c\Desktop\ds_and_algo\binary_tree6.PNG)

  * Pre-order traversal Binary Tree (전위순회)

    * Depth First Search

    * visit order: Root -> Left Subtree -> Right Subtree. 각 서브트리 내에서도 이 규칙이 적용됨

    * 예시 트리에서 순회 순서: 20 -> 100 -> 50 -> 222 -> 15 -> 3 -> 250 -> 35

    * ```
      preOrderTraversal(root) // T(n) T()는 뭐지....?
      	if (root equals null) // O(1)
      		return error // O(1)
      	else // O(1)
      		print root // O(1)
      		preorderTraversal(root.left) // T(n/2)
      		preorderTraversal(root.right) // T(n/2)
      ```

    * 시간복잡도: O(n) // 재귀함수 챕터를 다시 보라는데.... 이거 이해 잘 안 된다 질문하기!!

    * 공간복잡도: O(n) // 내부적으로 right node 같은 것 때문에 스택을 쓴다고!

      * ![binary_tree7](C:\Users\zoo2c\Desktop\ds_and_algo\binary_tree7.PNG)

  * In-order traversal Binary Tree (중위순회)

    * Depth First Search

    * Left Subtree -> Root -> Right Subtree

    * 222 -> 50 -> 100 -> 15 -> 20 -> 250 -> 3 -> 35

    * ```
      inOrderTraversal(root) // T(n)
      	if (root equals null) // O(1)
      		return // O(1)
      	else // O(1)
      		inOrderTraversal(root.left) // T(n/2)
      		print root // O(1)
      		inOrderTraversal(root.right) // T(n/2)
      ```

    * 시간복잡도: O(n)

    * 공간복잡도: O(n) // because of internal stack

  * Post-order traversal Binary Tree (후위순회)

    * Depth First Search

    * Left Subtree -> Right Subtree -> Root

    * 222 -> 50 -> 15 -> 100 ->  250 -> 35 -> 3 -> 20

      * ![binary_tree8](C:\Users\zoo2c\Desktop\ds_and_algo\binary_tree8.PNG)

    * ```
      postOrderTraversal(root) // T(n)
      	if (root equals null) // O(1)
      		return // O(1)
      	else // O(1)
      		postOrderTraversal(root.left) // T(n/2)
      		postOrderTraversal(root.right) // T(n/2)
      		print root // O(1)
      ```

    * 시간복잡도: O(n)

    * 공간복잡도: O(n) // 최악의 경우 모든 노드를 스택에 넣었다 빼야 할 수 있음

  * Level-order traversal Binary Tree (레벨순회)

    * Breadth First Search

    * 20 -> 100 -> 3 -> 50 -> 15 -> 250 -> 35 -> 222

    * ```
      levelOrderTraversal(root)
      	Create a Queue(Q)  // O(1) // 다른 순회 방법들과 다르게 큐를 사용함!
      	enqueue(root) // O(1)
      	while (Queue is not empty) // O(n)
      		enqueue() the child(children인 것 같기도....?!) of the first element // O(1)
      		dequeue() and print // O(1)
      ```

    * 시간복잡도: O(n) // while loop 안에서 모든 노드들을 큐에 넣었다 빼야 함

    * 공간복잡도: O(n) // 최악의 경우 모든 노드들이 다 큐에 들어가 있는 순간이 오기 때문에?!

  * Search for value in Binary Tree

    * 항상 레벨순회 방법을 씀. 큐를 쓰기 때문에. 큐는 스택보다 빠름. (저번시간에한거 다시읽어봐야할듯....ㅋㅋㅋㅋ)

    * ```
      searchForGivenValue(value)
      	if root == null // O(1)
      		return error message // O(1)
      	else // O(1)
      		do a level order traversal // O(n)
      			if value found // O(1)
      				return success message // O(1) // 매번 못찾으면 도로 디큐..?? 아님 디큐할 때 확인....???? 이 부분 잘 모르겠다. 아 디큐할 때 확인하는 거 맞나 봄..?!
      		return unsuccessful message // O(1)
      ```

    * 시간복잡도: O(n)

    * 공간복잡도: O(n)

  * Insert value in Binary Tree

    * 2 conditions

      * when the root is a blank // if the tree does not exists, create a new root node
      * insert at the first vacant child // 레벨순회, check whether the node is blank

    * ```
      insertNode(BinaryTree):
      	if root is blank // O(1)
      		insert new node at root // O(1)
      	else // O(1)
      		do a level order traversal and find the first blank space // O(n)
      		insert in that blank place // O(1)
      ```

    * 시간복잡도: O(n)

    * 공간복잡도: O(n)

  * Delete value from Binary Tree

    * 2 conditions

      * when the value to be deleted is not existing in the tree
      * when the value to be deleted exists in the tree
        * deepest node(레벨순회를 할 때 가장 나중에 나오는 노드)를 찾아서 지우려는 노드에 그 값을 집어넣고 deepest node 지우기. 왜냐하면 그냥 지우면 그 노드에 의존하고 있는 자식 노드들이 있기 때문에! 그래서 뭐라도 해야 한다고....??!! --> 사실 이거 뭔 말인지 이해 못 했음! 물어보기!!!!!
        * leaf는 상관없이 그냥 지워도 되는 듯

    * ```
      deleteNodeFromBinaryTree()
      	search for the node to be deleted // O(n)
      	find deepest node in the tree // O(n)
      	copy deepest node's data in current node // O(1)
      	delete deepest node // O(1)
      ```

    * 시간복잡도: O(n)

    * 공간복잡도: O(n)

  * Delete Binary Tree

    * 루트 노드만 지우면 됨!

    * ```
      deleteBinaryTree()
      	root = null
      ```

    * 시간복잡도: O(1)

    * 공간복잡도: O(1)

* Binary Tree (Array)

  * create

    * ```
      createBinaryTree()
      	create a blank array of 'size'
      	update lastUsedIndex to 0
      ```

    * 시간복잡도: O(1)

    * 공간복잡도: O(n)

  * insert value

    * 2 cases

      * if array is already full, return error message
      * insert at first vacant cell in array (위의 경우가 아닌 모든 경우인 듯. 항상 이런 방식으로(만) 하는 건가? 트리의 경우에는 원하는 위치에 집어넣는 일이 별로 없나...? 그리고 삭제의 경우에서 볼 수 있듯이 어느 값이 어느 위치에 있는가도 별로 안 중요한 건가?!?!)

    * ```
      insertValueInBinaryTree()
      	if Tree is full
      		return error message
      	else
      		insert value in first unused cell of array
      		update lastUsedIndex
      ```

    * 시간복잡도: O(1)

    * 공간복잡도: O(1)

  * search for value

    * 2 cases

      * when the value to be searched does not exists in the tree
      * when the value to be searched exists in the tree

    * ```
      searchValueInBinaryTree()
      	traverse the entire array from 1 to lastUsedIndex
              if value is found
                  return success message
      	return error message
      ```

    * 시간복잡도: O(n)

    * 공간복잡도: O(1)

  * In-order traversal of Binary Tree (중위순회)

    * Depth First Search

    * ```
      InorderTraversal(index) // T(n) // 맨 처음에는 인덱스가 1부터 시작함
      	if index > lastUsedIndex // O(1)
      		return // O(1)
      	else // O(1)
      		InorderTraversal(index*2) // T(n/2)
      		print current index.value // O(1)
      		InorderTraversal(index*2+1) // T(n/2)
      ```

    * 이 알고리즘 이해 안 됨.... ==> 아 이제 이해 될/되는 것 같기도!! 연결리스트로 구현했을 때의 코드랑 비교하면서 보기!!!!

    * 시간복잡도: O(n) // back substitution method를 쓴다고??!!??!! 이게 무슨 말이지

    * 공간복잡도: O(n) // 재귀적 실행을 처리하기 위해 내부적으로 스택을 사용하기 때문에

  * Pre-order traversal of Binary Tree (전위순회)

    * DFS

    * ```
      PreorderTraversal(index) // T(n)
      	if index > lastUsedIndex // O(1)
      		return // O(1)
      	else // O(1)
      		print current index.value // O(1)
      		InorderTraversal(index*2) // T(n/2)
      		InorderTraversal(index*2+1) // T(n/2)
      ```

    * 시간복잡도: O(n)

    * 공간복잡도: O(n)

  * post-order traversal of Binary Tree (후위순회)

    * DFS

    * ```
      PostorderTraversal(index) // T(n)
      	if index > lastUsedIndex // O(1)
      		return // O(1)
      	else // O(1)
      		InorderTraversal(index*2) // T(n/2)
      		InorderTraversal(index*2+1) // T(n/2)
      		print current index.value // O(1)
      ```

    * 시간복잡도: O(n)

    * 공간복잡도: O(n)

  * level-order traversal of Binary Tree (레벨순회)

    * BFS

    * ```
      levelOrderTraversal()
      	loop: 1 to lastUsedIndex
      		print current index.value
      ```

    * 트리를 배열로 구현한 경우에는 내부적으로 따로 큐를 사용하지 않음

    * 시간복잡도: O(n)

    * 공간복잡도: O(1)

  * delete node from Binary Tree

    * 2 cases

      * when the value to be deleted is not existing in the tree
      * when the value to be deleted exists in the tree

    * 연결리스트의 경우와 개념은 똑같지만 구현 방법이 약간 다른 듯. 연결리스트 구현의 경우와 달리 노드끼리 서로 의존하지 않기 때문에!

      * 맨 마지막 셀의 값을 지우고 싶은 값이 있는 셀로 복사한 다음에 맨 마지막 셀을 '삭제'하면 되는 듯 (null을 집어넣기? -> 가 아니라 lastUsedIndex를 한 칸 앞으로 당기기(1 빼기)!! 그럼 자동으로 '삭제'된 효과가 나는 듯)

    * ```
      deleteNodeFromBinaryTree()
      	search for desired value in array // O(n)
      		if value found
      			replace this cell's value with the last cell and update lastUsedIndex
      	return error message
      ```

    * 시간복잡도: O(n)

    * 공간복잡도: O(1)

  * delete Binary Tree

    * ```
      deleteBInaryTree()
      	set array as null
      ```

    * 시간복잡도: O(1)

    * 공간복잡도: O(1)

* Binary Tree array vs. linked list implementation

  * | Operations                    | Time Complexity (Array Implementation) | Space Complexity (Array Implementation) | Time Complexity (Linked List Implementation) | Space Complexity (Linked List Implementation) |
    | ----------------------------- | -------------------------------------- | --------------------------------------- | -------------------------------------------- | --------------------------------------------- |
    | Creation of Tree              | O(1)                                   | O(n)                                    | O(1)                                         | ***O(1)***                                    |
    | Insertion of value in Tree    | O(1)                                   | O(1)                                    | **O(n)**                                     | **O(n)**                                      |
    | Deletion of value from Tree   | O(n)                                   | O(1)                                    | O(n)                                         | **O(n)**                                      |
    | Searching for a value in Tree | O(n)                                   | O(1)                                    | O(n)                                         | **O(n)**                                      |
    | Traversing a Tree             | O(n)                                   | O(1)                                    | O(n)                                         | **O(n)**                                      |
    | Deleting entire Tree          | O(1)                                   | O(1)                                    | O(1)                                         | O(1)                                          |
    | Space Efficient?              | -                                      | No                                      | -                                            | ***Yes***                                     |

  * 각각의 구현 방법이 더 효율적인 상황들이 있음

    * 배열은 빠르고, 연결리스트는 공간을 효율적으로 사용할 수 있음
