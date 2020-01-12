---
layout: post
title:  "재귀"
---

Properties of Recursion:

- same operation is performed multiple times with different inputs
- in every step we try to make the problem smaller
- we mandatorily need to have a base condition, which tells system when to stop the recursion

shy should we learn recursion?

* it makes the code easy to write (compared to 'iterative') whenever a given problem  can be broken down into similar sub-problems.
* it is heavily used in Data Structures like Tree, Graphs, etc.
* it is heavily used in techniques like 'Divide and Conquer', 'Greedy', 'Dynamic Programming'.

format of a recursive function

* recursive case: case where the function recur.

* base case: case where the function does not recur.

* ```python
  def sample_recursion(params):
      if base_case:
          return base_case_value
      else:
          sample_recursion(modified_params)
  ```

how does recursion works internally?

* stack!

* ```python
  def foo(n):
      if (n<1):
          return
      else:
          foo(n-1)
      print("Hello World", n)

  foo(3)
  ```

* ```shell
  Hello World 1
  Hello World 2
  Hello World 3
  ```

factorial

* definition

  * factorial of a non-negative integer n
  * denoted by n!
  * product of all positive integers from 1 to n

* ```python
  def factorial(n):
      if n == 0: # base condition
          return 1
      return (n * factorial(n-1))
  ```

fibonacci series

* definition

  * a series of numbers in which each number is the sum of the two preceding numbers
  * first 2 numbers by definition are 0 and 1.
  * 0, 1, 1, 2, 3, 5, 8, 13, 21, ...

* ```python
  def fib(n):
      if n < 1:
          throw error
      elif n == 1 or n == 2:
          return n - 1
      else:
          return fib(n-1) + fib(n-2)
  ```

* (재귀함수는 수열의 점화식 같은 걸로 표현되는 문제들을 풀 때 유용하겠구나..?!)

recursion vs iteration

* compares space & time complexity

* | particulars                            | recursion | iteration |
  | -------------------------------------- | --------- | --------- |
  | space efficient?                       | no        | yes       |
  | time efficient?                        | no        | yes       |
  | ease of code (to solve sub-problems) ? | yes       | no        |

* 공간: iteration은 함수들의 스택을 쌓을 필요 없이 루프를 돌리면 되니까 (이거 이해 안 됨. 아까 iteration도 스택 쌓지 않았나..?? 아님 그것도 재귀였나.... 모르겠다)

* 시간(execution efficiency): 재귀는 스택의 push, pop operation을 계속하기 때문에

when to use/avoid recursion?

* use
  * when we can easily breakdown a problem into similar subproblem
  * when we are ok with extra overhead (both time and space) that comes with it
    * 오버헤드가 정확히 얼마나 일어나는지 직접 조사해 봐야겠다
    * 오버헤드를 예측할 수 없을 때는 최대한 재귀를 사용하지 말 것.
      * (예시를 들어 주셨는데 못 알아들음...)
  * when we need a quick working solution instead of efficient one.
* avoid
  * if the response to any of the above statements is NO, we should not go with recursion.

practical use of recursion

* stack
* tree - traversal / searching(Binary Search Tree) / insertion / deletion
* sorting - quick sort / merge sort
* divide and conquer
* dynamic programming
* etc.
