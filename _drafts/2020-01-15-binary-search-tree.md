---
layout: post
title:  "이진 탐색 트리 Binary Search Tree"
---

* 참고) 이 섹션에서 모든 BST는 다 LL로 구현할 것! 인터뷰나 학교에서도 많이 그런다고. 그러나 따로 배열로도 구현해 보기

* What & Why of BST

  * what is BST?
    * Binary Tree in which all the nodes follows the below-mentioned properties:
      * The left sub-tree of a node has a key less than or equal to its parent node's key.
      * The right sub-tree of a node has a key greater than to its parent node's key
    * ![bst](C:\Users\zoo2c\Desktop\ds_and_algo\bst.PNG)
  * why should we learn BST?
    * ![bst2](C:\Users\zoo2c\Desktop\ds_and_algo\bst2.PNG)
    * BST는 (연결리스트의 공간적 장점을 가져가면서도) O(n)을 O(logn)으로 줄여줄 수 있음!

* Creation of a BST

  * ```
    createBST()
    	initialize Root with null
    ```

  * 시간복잡도: O(1)

  * 공간복잡도: O(1)

* Searching for a value in BST

  * BST에서는 삽입 전에도 탐색을 해야 하기 때문에 탐색을 먼저 배움!

  * ```
    searchBST(root, value): // T(n)
    	if (root is null) // O(1)
    		return null // O(1)
    	else if (root == value) // O(1)
    		return root // O(1)
    	else if (value < root) // O(1)
    		searchBST(root.left, value) // T(n/2) // 문제를 계속 반으로 쪼개고 있음
    	else if (value > root) // O(1)
    		searchBST(root.left, value) // T(n/2)
    ```

  * 시간복잡도: O(logn) // 적어진다는 건 알겠는데 왜 logn인지는 아직 잘 이해 못 함. 검색해 보기!!!!!

  * 공간복잡도: O(n) // because of recursive call

* Traversing a BST // 그냥 이진트리 때와 같음!

  * DFS

    * PreOrder Traversal

      * ```
        preorderTraversal(root)
        	if (root equals null)
        		return error message
        	else
        		print root
        		preorderTraversal(root.left)
        		preorderTraversal(root.right)
        ```

      * 시간복잡도: O(n) // 아하 back substitution method가 뭔지 알려면 time complexity에 대해 다루는 섹션을 다시 보라고....????!!

      * 공간복잡도: O(n)

    * InOrder Traversal

      * ```
        inorderTraversal(root)
        	if (root equals null)
        		return error message // return
        	else
        		inorderTraversal(root.left)
        		print root
        		inorderTraversal(root.right)
        ```

      * 시간복잡도: O(n)

      * 공간복잡도: O(n)

    * PostOrder Traversal

      * ```
        postorderTraversal(root)
        	if (root equals null)
        		return error message
        	else
        		postorderTraversal(root.left)
        		postorderTraversal(root.right)
        		print root
        ```

      * 시간복잡도: O(n)

      * 공간복잡도: O(n)

  * BFS

    * LevelOrder Traversal

      * ```
        levelOrderTraversal(root)
        	Create a Queue(Q)
        	enqueue(root)
        	While (Queue is not empty)
        		dequeue() and print
        		enqueue() the child of dequeued element // child가 아니고 children인 것 같은데... 어쨌든 직접 구현을 해 봐야겠다
        ```

      * 시간복잡도: O(n)

      * 공간복잡도: O(n) // 갑자기 이거 또 이해가 안 된다..!!

* Inserting a node in BST

  * 2 cases

    * BST is blank
    * BST is non-blank

  * ```
    insertBST(currentNode, valueToInsert) // T(n)
    	if (currentNode is null) // O(n)
    		create a node, insert 'valueToInsert' in it // O(n)
    	else if (valueToInsert <= currentNode's value) // O(n)
    		currentNode.left = insertBST(currentNode.left, valueToInsert) // T(n/2)
    	else // O(n)
    		currentNode.right = insertBST(currentNode.right, valueToInsert) // T(n/2)
    	return currentNode // O(n)
    ```

  * 재귀적 호출 때문에 내부적으로 스택을 씀

  * ![bst3](C:\Users\zoo2c\Desktop\ds_and_algo\bst3.PNG)

  * 시간복잡도: O(logn) // 아직도 이해 x... 꼭 인터넷 검색해 보기!!!!!!!!!!!!

  * 공간복잡도: O(logn) // 내부적으로 쓰는 스택 때문에. logn만큼의 노드를 집어넣었다 뺄 수 있기 때문에

* Deleting a node from BST

  * 3 cases

    * 1) node to be deleted is a leaf node
      * 삭제하려는 노드까지 온 다음, 자식이 없으면 그냥 지우면 됨(null로 바꿈)!
    * 2) node to be deleted has 1 child (자식이 아닌 그 아래의 자손 노드들은 상관 없음)
      * 지우려는 노드의 부모 노드의 자식을, 지우려는 노드의 자식 노드로 바꾸면 됨 (즉, 부모의 자식을 원래 그 부모의 손자로 다시 링크해 주면 됨)
    * 3) node to be deleted has 2 children
      * 지우려는 노드의 successor(이게 뭐더라? 이진트리 섹션에 나와 있던가.... 아하 중위순회에서 바로 다음에 나올 노드니까, 이진트리의 경우는 지울 노드 다음으로 큰 값을 가진 노드겠군..!근데 predecessor를 써도 되는 건가....????????!!!!!!!! 아하 써도는 되겠지만 그런 거꾸로 된 순서로 가는 순회 방법이 위에서 안 나와서 그런가....???? 그러면 같은 값들을 가지고도 여러 형태의 BST가 나올 수 있다는 건가....??!! 초기 값(root)이 중요한 건가)를 찾아서 지우려는 노드의 값을 successor의 값으로 바꾼 다음 원래의 successor를 삭제하면 됨
      * successor가 leaf node가 아닌 경우에도, 값을 바꾸는 것까지는 똑같이 한 다음 2)를 해 주면 됨!
      * 근데 그럼 또 자식이 2명일 수는 없는 건가....? 아 더 이상 왼쪽 자식 노드가 없구나..!!!!!!!!

  * ```
    deleteNodeFromBSt(root, valueToBeDeleted): // T(n). 주석으로 T()나 O()을 표시하지 않은 줄들은 전부 O(1)
    	if (root == null) return null;
    	if (valueToBeDeleted < root.value)
    		then root.left = deleteNodeFromBST(root.left, valueToBeDeleted) // T(n/2)
    	else if (valueToBeDeleted > root.value)
    		then root.right = deleteNodeFromBST(root.right, valueToBeDeleted) // T(n/2)
    	else // if currentNode is the node to be deleted
    		if root has both children // 3)
    			then find minimum element from right subtree // O(logn). logn은 트리의 height인데, 최악의 경우 successor를 찾으러 끝까지(leaf node까지) 내려갈 수도 있으니까
    			replace current node with minimum node from right subtree and delete minimum node from right
    		else if nodeToBeDeleted has only left child // 2)
    			then root = root.left()
    		else if nodeToBeDeleted has only right child // 2)
    			then root = root.right()
    		else // 1). if nodeToBeDeleted does not have any children
    			root = null;
    	return root
    ```

  * 시간복잡도: O(logn) // T(n)인데, O(logn)이므로. 따라서 back substitution method 때문에........????!!!!

  * 공간복잡도: O(logn) // because of the internal stack. ***logn means the height of the tree.***

* Deleting a BST

  * ```
    deleteBST()
    	root = null
    ```

  * 시간복잡도: O(1)

  * 공간복잡도: O(1)
