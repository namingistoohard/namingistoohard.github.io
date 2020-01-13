---
layout: post
title:  "재귀 Recursion"
date:   2020-01-12 23:54:07 +0900
---

> 이 글은 Udemy의 [Data Structures & Algorithms !](https://www.udemy.com/course/learn-data-structure-algorithms-with-java-interview/) 강의를 바탕으로 작성했습니다.

### 재귀란?
* 같은 operation이 다른 입력값에 대해 여러 번 실행되는 것
* 매번 문제를 더 작게 만드는 것
* 프로그램이 끝없이 돌다가 맛이 가지 않게 하려면 base condition이 반드시 필요하다.
- 문제를 비슷한 하위 문제로 계속 작게 쪼개는 방법. 따라서 코드를 작성하기 쉽다.
- 트리, 그래프, 분할정복법, 그리디 알고리즘, 동적 프로그래밍 등 많은 자료구조와 알고리즘에서 쓰이는 방법

### 재귀함수의 format
* recursive case: case where the function recur.
* base case: case where the function does not recur.

```python
def sample_recursion(params):
    if base_case:
        return base_case_value
    else:
        sample_recursion(modified_params)
```

재귀함수는 내부적으로 stack 자료구조를 이용해 작동한다.

```python
def foo(n):
    if n < 1:
        return
    else:
        foo(n-1)
    print("Hello World", n)
```

```shell
>>> foo(3)
Hello World 1
Hello World 2
Hello World 3
```

### 팩토리얼 Factorial

이란?
* 0 이상의 정수에 대해서만
* n!으로 표기
* n! = 1부터 n까지 곱한 결과값

```python
def factorial(n):
    if n == 0: # base condition
        return 1
    return n * factorial(n-1)
```

### 피보나치 수열 Fibonacci Series

이란?
* 수열의 각 항은 직전 두 항의 합이다.
* 첫 두 항은 0, 1이다.
* 0, 1, 1, 2, 3, 5, 8, 13, 21, ...

```python
def fibonacci(n):
    if n < 1:
        raise ValueError
    elif n == 1 or n == 2:
        return n - 1
    else:
        return fibonacci(n-1) + fibonacci(n-2)
```

(재귀함수는 수열의 점화식 같은 걸로 표현되는 문제들을 풀 때 유용하겠구나..?!)

### recursion vs iteration
* compares space & time complexity

| particulars | recursion | iteration |
| --- | --- | --- |
| space efficient? | no | yes |
| time efficient? | no | yes |
| ease of code (to solve sub-problems)? | yes | no |


공간: iteration은 함수들의 스택을 쌓을 필요 없이 루프를 돌리면 되니까 (이거 이해 안 됨. 아까 iteration도 스택 쌓지 않았나..?? 아님 그것도 재귀였나.... 모르겠다)

시간(execution efficiency): 재귀는 스택의 push, pop operation을 계속하기 때문에

### when to use/avoid recursion?
- 문제를 비슷한 subproblem으로 쪼갤 수 있을 때
- 재귀의 사용으로 인한 시/공간 소모 overhead를 예측할 수 있을 때
- 문제를 빠르게 해결하고 싶을 때 (efficient하지는 않음)
- 이 중 하나라도 해당하지 않는다면, 재귀를 사용하지 말 것!

### 재귀의 사용 예시
- 스택
- 트리의 순회/탐색(이진 탐색 트리)/삽입/삭제
- 분할정복법
- 동적 프로그래밍
