---
layout: post
title:  "알고리즘의 시간 복잡도"
---

> 이 글은 Udemy의 [Data Structures & Algorithms !](https://www.udemy.com/course/learn-data-structure-algorithms-with-java-interview/) 강의를 바탕으로 작성했습니다.

* what
  * a study of a given algorithm's running time, by identifying its behavior as the input size for the algorithm increases. In a layman's language we can say, 'how much time will the given algorithm will take to run.
  * 인풋의 크기가 늘어남에 따라서 알고리즘이 어떻게 행동(?)하는지
* why
  * 알고리즘의 efficiency를 측정하기 위해서
  * 이 run time analysis에 대해서 잘 모르는 상태로 비효율적인 코드를 짠다면, 컴퓨터가 코드를 실행하다가 맛이 가 버릴 것이다.

### algo run time analysis 표기법

차의 연비에 비유해 생각할 수 있다. 같은 차라도 어디를 달리는지에 따라 연비가 달라진다. 오프로드에서는 연비가 최악이 될 것이고, 깨끗한 고속도로 위에서는 연비가 최악이 될 것이다. 중간 상태?에서는 연비도 중간이 될 것이고... 알고 표기법에도 이렇게 3가지가 있다.

#### 빅-오메가(Big-Omega) 표기법 (Ω)
* 최상의 인풋을 가정한다.
* ex) 이 알고리즘에 100개의 인풋이 들어가면, 항상 최소 10초는 걸릴 것이지만 10초 이하로 걸리는 경우는 없다.
* lower bound
* will guarantee the minimum time 알고리즘이 실행되는 데 걸리는

#### Big-o (O)
* this notation gives us the tighter upper bound of a given algorithm.
* in a layman's language we can say that for any given input, running time of a given algorithm will not be <u>more than</u> given time.
* 최대 100초가 걸릴 것이다. (worst case)
* 'more than' any given time (?)
* 그래서 보통 여기에 맞춰서 어플리케이션을 개발하는 듯? exceed하지 않도록
* 그래서 이거를 많이 효율성의 기준으로 삼음

#### theta (그리스 문자 세타) Θ
* 평균 이 정도는 걸린다

세 표기법 모두 학문적으로는 의미 있는 것들이지만, 항상 시간에 쫓기며 스파게티 코드를 생산해 내는 개발자들에게는 최소한 컴퓨터가 죽지만은 않았으면 좋겠다는 생각을 하고 있을 것이다~~ 따라서 보통은 빅오가 가장 유명하고 많이 쓰인다.

#### 예시
길이가 n인 배열에서 a라는 값을 찾아야 하는 경우,

`Ω(1)`: 최선의 경우. 즉 a가 배열의 맨 처음(인덱스 0)에 존재할 경우

`O(n)`: 최악의 경우. 즉 a가 배열의 맨 마지막(인덱스 n-1)에 존재할 경우

`Θ(n/2)`: 모든 경우의 평균. 대략 n이 배열의 중간 지점에 위치하는 경우와 비슷할 것이다.


examples of algorithm run time complexities

Time Complexity | Name | Example
--- | --- | ---
O(1) | Constant | Adding and element at front of linked list
O(logn) | Logarithmic | Finding an element in sorted array
O(n) | Lineear | Finding an elemetn in unsorted array
O(nlogn) | Linear Logarithmin | Merge Sort
O(n^2) | Quadratic | Shortest path between 2 nodes in a graph
O(n^3) | Cubic | Matrix Multiplication
O(2^n) | Exponential | Tower of Hanoi Problem

how to calculate run time complexity of a given algorithm?

* iterative algorithm

```java
int findBiggestNumber(int[] arr) { // 문법이 맞나 모르겠네,,,,
    int biggestNumber = arr[0]; // O(1)
    for (int i=1; i<arr.length; i++) { // O(n)
        if (arr[i] > biggestNumber) { // O(1)
            biggestNumber = arr[i]; // O(1)
        }
    }
    return biggestNumber; // O(1)
}
```
시간복잡도 = O(n)

O(n) = O(n-1) = O(n-100). n이 커지면 상수는 의미가 없다.


* recursive algorithm

  * 문제 1

```
FindBiggestNumber(A, n): // T(n)
    static highest = Integer.Min // O(1)
    if n equals -1 // O(1)
    return highest // O(1)
    else // O(1)
    if A[n] > highest // O(1)
        update highest // O(1)
    return FindBiggestNumber(A, n-1) // T(n-1)
```
T()에 대해 설명하기! Back substitution


  * 문제 2: 11개의 숫자가 정렬된 어레이에서 110이 없는지 찾아라.

  * binary search를 쓴다.

    * 찾는 값이 중간값보다 크면 오른쪽 숫자들 중에 또 가운데 숫자를 찾고, ....
    * 개수가 짝수면 어느 쪽을 볼 건지 골라야 함

```
binarySearch(int findNumber, int[] arr, start, end): # T(n)
    if (start equals end): # O(1)
        if (arr[start] equals findNumber): # O(1)
            return start # O(1)
        else: # O(1)
            return error message # number does not exists in the array # O(1)

    mid = findMid(arr, start, end) # O(1)
    if mid > findNumber # O(1)
        binarySearch(int findNumber, int[] arr, start, mid) # T(n/2)
    elif mid < findNumber # O(1)
        binarySearch(int findNumber, int[] arr, mid, end) # T(n/2)
    elif mid == findNumber # O(1)
        return mid # O(1)
```

* T(n/2^k) 자리에 1을 대입해서 T(1)
    * n / 2^k = 1
    * n = 2^k
    * k = log n
* (두 번째 문제 이해 잘 못 함.... 열심히 안 들어서)
