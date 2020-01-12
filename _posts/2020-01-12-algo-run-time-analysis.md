---
layout: post
title:  "알고리즘의 시간 복잡도"
---

* what
  * a study of a given algorithm's running time, by identifying its behavior as the input size for the algorithm increases. In a layman's language we can say, 'how much time will the given algorithm will take to run.
* why
  * to measure 'efficiency' of a given algorithm.
  * if we don't learn this topic, our program will be easily exhausted.

notations for algo run time analysis

* car example: how much does this car runs on 1 litre of petrol?
  * in city traffic? worst case scenario, large sum of data (10)
  * on highway? best case scenario (20)
  * mixed environment? average scenario(15)
  * 연비는 상황에 따라 달라질 수 있음
* 3 notations for run time analysis
  * Omega (오메가 기호)
    * this notation gives the tighter lower bound of a given algorithm.
    * in a layman's language we can say that for any given input, running time of a given algorithm will not be <u>less than</u> given time.
    * 1000개의 인풋이 들어가면, 10초 이상은 걸릴 수 있어도 10초 이하로 걸리는 경우는 없다. (?????)
    * minimum is required.
    * will guarantee the minimum time 알고리즘이 실행되는 데 걸리는
  * Big-o (O)
    * this notation gives us the tighter upper bound of a given algorithm.
    * in a layman's language we can say that for any given input, running time of a given algorithm will not be <u>more than</u> given time.
    * 최대 100초가 걸릴 것이다. (worst case)
    * 'more than' any given time (?)
    * 그래서 보통 여기에 맞춰서 어플리케이션을 개발하는 듯? exceed하지 않도록
    * 그래서 이거를 많이 효율성의 기준으로 삼음
  * theta (그리스 문자 세타)
    * this notation decides whether upper bound and lower bound of a given algorithm are same or not.
    * in a layman's language we can say that for any given input, running time of a given algorithm will <u>on an average</u> be equal to given time.

examples of notations

* 길이가 n인(원소가 n개인) 어떤 배열에 10이 존재하는지 찾아서 그 인덱스를 반환하는 데는 n time(?, n개의 단위 시간)이 걸릴 것이다.
  * n x 1, => n unit-time
* omega(1) (10이 배열의 맨 처음에 있을 때, 최선의 경우)
* O(n) (10이 배열의 맨 끝에 있을 떄, 최악의 경우)
* theta(n/2) (평균, 10이 배열의 중간에 있는 것과 비슷한 경우)
* 아카데믹한 경우에는 셋 다 알아야 하겠지만, 실제 상황에서는 big-o가 중요함

examples of algorithm run time complexities

* ![algo_run_time_complexities](C:\Users\zoo2c\Desktop\ds_and_algo\algo_run_time_complexities.png)
* ![algo_run_time_complexities_2](C:\Users\zoo2c\Desktop\ds_and_algo\algo_run_time_complexities_2.png)

how to calculate run time complexity of a given algorithm?

* iterative algorithm

  * ```java
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

  * ![algo_run_time_complexities_3](C:\Users\zoo2c\Desktop\ds_and_algo\algo_run_time_complexities_3.png)

  * => time complexity = O(n)

  * O(n) = O(n-1) = O(n-2). 상수는 미분할 때처럼 떼어 버려도 괜찮음

* recursive algorithm

  * 문제 1

  * ```
    FindBiggestNumber(A, n): // T(n)
      static highest = Integer.Min // O(1)
      if n equals -1 // O(1)
        return highest // O(1)
      else // O(1)
        if A[n] > highest // O(1)
          update highest // O(1)
      return FindBiggestNumber(A, n-1) // T(n-1)
    ```

  * ![algo_run_time_complexities_4](C:\Users\zoo2c\Desktop\ds_and_algo\algo_run_time_complexities_4.png)

  * 문제 2: 11개의 숫자가 정렬된 어레이에서 110이 없는지 찾아라.

  * binary search를 쓴다.

    * 찾는 값이 중간값보다 크면 오른쪽 숫자들 중에 또 가운데 숫자를 찾고, ....
    * 개수가 짝수면 어느 쪽을 볼 건지 골라야 함

  * ![algo_run_time_complexities_5](C:\Users\zoo2c\Desktop\ds_and_algo\algo_run_time_complexities_5.png)

  * ![algo_run_time_complexities_6](C:\Users\zoo2c\Desktop\ds_and_algo\algo_run_time_complexities_6.png)

  * ![algo_run_time_complexities_7](C:\Users\zoo2c\Desktop\ds_and_algo\algo_run_time_complexities_7.png)

    * T(n/2^k) 자리에 1을 대입해서 T(1)
      * n / 2^k = 1
      * n = 2^k
      * k = log n
    * (두 번째 문제 이해 잘 못 함.... 열심히 안 들어서)
