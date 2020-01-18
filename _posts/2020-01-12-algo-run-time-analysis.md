---
layout: post
title:  "알고리즘 성능 분석 Algorithm Run Time Analysis"
date:   2020-01-12 23:17:16 +0900
author: gakyeong
tags: [algorithm]
---

> 이 글은 Udemy의 [Data Structures & Algorithms !](https://www.udemy.com/course/learn-data-structure-algorithms-with-java-interview/) 강의를 바탕으로 작성했습니다.

### 알고리즘 성능 분석이란?
입력값의 크기가 늘어남에 따라 알고리즘이 시간과 메모리를 얼마나 사용하는지 분석하는 것이다.
시간에 대한 성능 분석을 **시간 복잡도**라고 하고, 메모리에 대한 성능 분석을 **공간 복잡도**라고 한다.

#### 알고리즘 성능 분석이 왜 필요한가?
알고리즘의 효율성을 측정하기 위해서이다. 만약 알고리즘의 성능을 잘 알지 못하는 상태로 비효율적인 코드를 짠다면, 컴퓨터가 코드를 실행하는 도중에 부하가 걸려서 멈춰 버릴 수도 있다.


### 알고리즘 복잡도 표기법
알고리즘의 복잡도를 표현하는 방법은 차의 연비에 비유해 생각할 수 있다. 같은 자동차도 어디를 달리는지에 따라 연비가 달라진다. 오프로드에서는 연비가 최악이 될 것이고, 깨끗한 고속도로 위에서는 최고가 될 것이다. 그리고 중간 상태(?)의 길 위에서는 연비도 중간이 될 것이다. 알고리즘의 복잡도를 표현하는 방식도 이와 비슷하다. 여기서는 가장 많이 쓰이는 세 가지를 살펴 볼 것이다.

#### 빅-오메가 표기법 Big-Ω Notation
* `Ω()`로 표기
* 최상의 인풋을 가정한다. 즉, 알고리즘을 살행하는 데 걸리는 최소 시간을 나타낸다.
* ex) 이 알고리즘에 100개의 인풋이 들어가면, 항상 최소 10초는 걸릴 것이지만 10초 이하로 걸리는 경우는 없다.

#### 빅-오 표기법 Big-O Notation
* `O()`로 표기
* 최악의 인풋을 가정한다. 즉, 알고리즘을 살행하는 데 걸리는 최대 시간을 나타낸다.
* ex) 이 알고리즘에 100개의 인풋이 들어가면, 최악의 경우 100초가 걸릴 것이다.

#### 빅-세타 표기법 Big-Θ Notation
* `Θ()`로 표기
* 평균 이 정도는 걸린다

세 표기법 모두 학문적으로는 의미 있는 것들이지만, 항상 시간에 쫓기며 스파게티 코드를 생산해 내는 개발자들에게는 최소한 컴퓨터가 맛이 가 버리지 않는 것이 중요하기 때문에 보통은 Big-O 표기법이 효율성의 기준으로 통용된다.

#### 예시
길이가 `n`인 배열에서 `a`라는 값을 찾아야 하는 경우, 이 세 가지 표기법으로는 각각 아래와 같이 표기할 수 있다.

`Ω(1)`: 최선의 경우. 즉 a가 배열의 맨 처음(인덱스 0)에 존재할 경우

`O(n)`: 최악의 경우. 즉 a가 배열의 맨 마지막(인덱스 n-1)에 존재할 경우

`Θ(n/2)`: 모든 경우의 평균. 대략 n이 배열의 중간 지점에 위치하는 경우와 비슷할 것이다.


#### 알고리즘의 시간 복잡도 표기 예시 (Big-O)

시간 복잡도 | 이름 | 예시
--- | --- | ---
O(1) | 상수 시간 Constant time | 연결 리스트에 노드 삽입
O(logn) | 로그 시간 Logarithmic time | 정렬된 배열에서 주어진 값 찾기
O(n) | 선형 시간 Linear time | 정렬되지 않은 배열에서 주어진 값 찾기
O(nlogn) | 선형 로그 시간 Linear Logarithmic time | 합병 정렬
O(n^2) | 2차 시간 Quadratic time | 그래프에서 두 노드 간의 최단 거리 구하기
O(n^3) | 3차 시간Cubic time | 행렬곱
O(2^n) | 지수 시간 Exponential time | 하노이의 탑 문제

### 알고리즘의 시간 복잡도는 어떻게 계산하는가?

#### 반복문

```java
int findBiggestNumber(int[] arr) {
    int biggestNumber = arr[0]; // O(1)
    for (int i=1; i<arr.length; i++) { // O(n)
        if (arr[i] > biggestNumber) { // O(1)
            biggestNumber = arr[i]; // O(1)
        }
    }
    return biggestNumber; // O(1)
}
```
* 시간복잡도 = O(n)
* `O(n) = O(n-1) = O(n-100)`. n이 충분히 커지면 상수는 의미가 없다.


#### 재귀 함수 - 1

```java
int findBiggestNumber(arr, n): // T(n)
    static highest = Integer.Min // O(1)
    if (n == -1) { // O(1)
        return highest; // O(1)
    } else { // O(1)
        if (arr[n] > highest) { // O(1)
            highest = arr[n]; // O(1)
        } // O(1)
    }
    return findBiggestNumber(arr, n-1) // T(n-1)
```
`T()`은 후진 대입법backward substitution을 위한 것이라고 한다. 정확하게 무엇인지는 잘 모르겠어서 더 찾아봐야겠다.

#### 재귀 함수 - 2

문제: 11개의 숫자가 정렬된 배열에서 110을 찾아라.
* binary search를 쓴다.

```java
int binarySearch(int findNumber, int[] arr, int start, int end) { // T(n)
    if (start == end) { // O(1)
        if (arr[start] == findNumber) { // O(1)
            return start; // O(1)
        } else { // O(1)
            throw new Exception("The number does not exists in the array"); // O(1)
        }
    }

    int mid = findMid(arr, start, end); // O(1)
    if (mid > findNumber) { // O(1)
        binarySearch(findNumber, arr, start, mid); // T(n/2)
    } else if (mid < findNumber) { // O(1)
        binarySearch(findNumber, arr, mid, end); // T(n/2)
    } else if (mid == findNumber) { // O(1)
        return mid; // O(1)
    }
}
```

* T(n/2^k) 자리에 1을 대입해서 T(1)
    * n / 2^k = 1
    * n = 2^k
    * k = log n
* (두 번째 문제 이해 잘 못 함.... 열심히 안 들어서)
