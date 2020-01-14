---
layout: post
title:  "재귀 Recursion"
date:   2020-01-12 23:54:07 +0900
---

> 이 글은 Udemy의 [Data Structures & Algorithms !](https://www.udemy.com/course/learn-data-structure-algorithms-with-java-interview/) 강의를 바탕으로 작성했습니다.

### 재귀란?
* 같은 작업(함수)이 다른 입력값에 대해 여러 번 실행되는 것
* 문제를 비슷한 하위 문제로 계속 작게 쪼개서 해결하는 방법. 따라서 코드를 작성하기 쉽다.
* 스택, 트리, 그래프, 분할정복법, 그리디 알고리즘, 동적 프로그래밍 등 많은 자료구조와 알고리즘에서 쓰이는 방법

### 재귀함수의 구조
* recursive case: 함수가 재귀적으로 호출되어야 할 경우.
* base case: 함수가 재귀적으로 호출되지 말아야 할 경우. 이 base case가 없다면 컴퓨터가 무한히 함수를 실행하다가 맛이 가 버리고 말 것이다.

```python
def sample_recursion(params):
    if base_case:
        return base_case_value
    else:
        sample_recursion(modified_params)
```

재귀함수는 내부적으로 스택 자료구조를 이용해 작동한다.

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

* 0 이상의 정수에 대해서만
* `n!`으로 표기
* n! = 1부터 n까지 곱한 결과값

```python
def factorial(n):
    if n == 0: # base condition
        return 1
    return n * factorial(n-1)
```

### 피보나치 수열 Fibonacci Series

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

재귀함수는 수열의 점화식과 같은 형식으로 표현할 수 있는 문제들을 풀 때 유용할 것 같다. → 라고 생각했는데 점화식이 영어로 recurrence relation이었다..! ㅎㅎ

### 재귀 vs. 반복

| | recursion | iteration |
| --- | --- | --- |
| space efficient? | no | yes |
| time efficient? | no | yes |
| ease of code (to solve sub-problems)? | yes | no |

재귀 함수는 내부적으로 사용하는 스택의 push, pop을 계속하기 때문에, 시간적/공간적 측면 모두에서 반복문보다 느리다.

### 언제 재귀 함수를 사용해야 하는가?
- 문제를 비슷한 하우 문제들로 쪼갤 수 있을 때
- 재귀의 사용으로 인한 시/공간 오버헤드를 예측할 수 있을 때
- 문제를 빠르게 해결하고 싶을 때

이 중 하나라도 해당하지 않는다면, 재귀를 사용하지 말 것!
