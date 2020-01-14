우선 재귀 알고리즘과 메모이제이션 알고리즘을 자바 수도코드로 만들어 보려고 한다.

1. 재귀 알고리즘
```
recursive algorithm = 
A recursive algorithm is an algorithm which calls itself with "smaller (or simpler)" input values,
and which obtains the result for the current input by applying simple operations to the returned value
for the smaller (or simpler) input.
```

음, 아무튼 재귀함수는 자기 자신을 다시 호출하는 함수라는 것은 알겠다.

```java

class void recur(){


  return recur();
}

```

일단 이렇게 만들어 보았다.
재귀 알고리즘에는 또 하나의 특성이 있는데, 만약 재귀를 탈출 하지 못하면 무한루프에 진입한다.
따라서 탈출이 가능한 base case를 만들어주자.

```java

class void recur(){
  
  if(base_case){
    return;
  }else{
    return recur();
  }
}

```

재귀함수가 완성되었다!

2. 메모이제이션

메모이제이션이란 "프로그래밍을 할 때 반복되는 결과를 메모리에 저장해서 다음에 같은 결과가 나올 때 빨리 실행하는 코딩 기법을 말합니다." (출처 인터넷)

최근에 푼 문제들에서는 메모이제이션에서 주로 1차원 배열을 사용했다.
즉, 구해야 하는 값들의 범위가 a 부터 b까지 라고 한다면, a~b까지의 배열을 만들고 만약 이미 계산된 그 사이의 값에 대한 결과는 이미
저장되있기 때문에 다시 계산을 하지 않아도 되는 것이다.

이 메모이제이션은 공간 복잡도가 정해져 있는 것 처럼 보인다. 그리고 시간복잡도도 해당 인덱스를 호출하기만 하면 된다.

코드로는 특별히 구현할 것은 없다.

```java

static object [] memo = new object [range];

class test{
  public static void main (String[] args){
  
   . . .
   

   if (memo[i] != null){
       result = memo[i];
   }else{
       result = solve(i);
   }
   
   . . .
  
  }
}

```

자바에 대해 풀다 보게 되니, 자바의 구조 자체도 뭔가 이야기 해야 될 것같다.

static 이나 primitive 자료형, 객체지향 구조 등.. 다음에 풀어봐야 겠다.
