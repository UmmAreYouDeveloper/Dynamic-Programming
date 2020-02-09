# Dynamic Programming

## Introdution

`큰 문제를 작은 문제로 나눠서 푸는 알고리즘`

> `<< DP와 분할정복의 차이 >>`
>   >1. 다이나믹 프로그래밍 - 문제를 나눠도 문제의 크기가 중복될 수있음
>
>   >2. 분할 정복 - 문제를 나누면 이전에 나왔던 문제의 크기가 중복될 수 없음

## Condition

`이 문제가 다이나믹 프로그래밍기법으로 해결이 가능한가?`

> `<< 다음의 2가지 조건을 만족 >>`
>
> __1. Overlapping Subprobelm(겹치는 부분문제)__
>   >중복되는 부분(작은)문제들로 큰 문제를 나눌수 있다.
>
> __2. Optimal Substructure(최적 부분구조)__
>   >작은문제들의 정답으로 큰 문제의 정답을 도출할 수 있어야 한다.
>
> __3. 예시__
>   >피보나치 수열 Fn = Fn-1 + Fn-2  
>   >   >큰문제(n)을 작은 문제(n-1, n-2)의 정답을 더해서 구할수 있다.(optimal substructure)
>   >
>   >   >n-1은 다시 n-2와 n-3으로 쪼개지기 때문에 n-2크기의 작은문제가 중복된다!(overlapping subproblem)

## Time complexity

`점화식으로 시간복잡도 구해보기`

> __문제의 개수(크기) X 문제 1개를 푸는 시간__

## Feature
>   > 다이나믹 프로그래밍에서 각 문제는 한 번만 풀어야 한다.
>   >
>   > Optimal Substructure를 만족하기 때문에, 같은 문제는 구할 때마다 장답이 같다. -> 피보나치 수 같은거 F10 구할때의 F9 F8과 F11구할 때의 F10 F9에서 F9가 달라지지않는다.
>   >
>   > 따라서, 같은 작업을 또 할 필요는 없기에, 정답을 어딘가에 메모해놓는다.
>   >
>   > 이런 메모하는 것을 코드의 구현에서는 배열에 저장하는 것으로 할 수 있다.
>   >
>   > 메모를 한다고 해서 영어로 Memoization이라고 한다.

## Implementation Method
>   `Top - down`   
>   >1. 큰 문제를 작은 문제로 나눈다.
>   >2. 작은 문제를 푼다.
>   >3. 작은 문제를 풀었으니, 이제 큰 문제를 푼다.
>   > 주로 recursive로 구현한다. & Memoization 배열 필요.
>
>   `Bottom - up`
>   > 1. 문제를 크기가 작은 문제부터 차례대로 푼다.
>   > 2. 문제의 크기를 조금씩 크게 만들면서 문제를 점점 푼다.
>   > 3. 작은 문제를 풀면서 왔기 때문에, 큰 문제는 항상 풀 수 있다.
>   > 3. 반복하다 보면 가장 큰 문제를 풀 수 있다.
>   > 주로 반복문으로 구현
>
>   `두 방식의 차이`
>   > 1. 시간차이 => 알 수 없음
>   >   > 재귀가 느린 알고리즘 같지만 오히려 Bottom - up은 하나하나 다하기 때문에 더 오래걸릴 수 있음
>   >   > 재귀도 Memoization으로 함수 호출을 감소시키기 때문에 어떻게 될지 알 수없다.
>   > 2. Stack overflow
>   >   >Python은 위험
>   >   >C++이나 Java는 괜찮다.

## Problem-solving strategy
>   `1. 문제에서 구하려고 하는 답을 문장으로 나타낸다.`
```
dp[i] = i번째 피보나치 수

dp[i][j] = 끝자리 숫자가 j이고 i길이의 숫자

```

>   `2. 문장에 나와 있는 변수의 개수 만큼 메모하는 배열을 만든다.`
```
N크기의 문제 => n번째 무엇인가를 구하시오.

vector<int> dp(n);
```

>   `문제를 작은 문제로 나누고, 수식을 이용해서 문제를 표현해야 한다.(점화식)`
```
O + O + O + .... + ``O(N-1번째)`` = N
이라고 할 때, ``O(N-1번째)``에 무엇이 들어갈지를 생각해본다. => 경우의 수를 생각

<< 문제를 작은 문제로 쪼개는 법 - dp배열 인덱싱 >>
DP[N] => N번째 경우의 답이므로 N이 어떻게 작아 지는가 본다.
이를 테면,
1씩 길이가 줄어든다. => N-1
2배씩 감소한다. => N/2
...

문제를 쪼개는 기술은 보통,
(항상 N과 그 전단계) + `(첫번째 부터 전 단계 2개로 쪼갠다.)`
                                        ^    
    ____________________________________I    
    I            
    v            
`(전단계 전전 단계)` + (첫번째부터 전전 단계)
...이런 방식으로 계속 쪼개진다.

차원을 높인다는 것은 문제의 변수가 증가한다는 것을 의미
dp[i] => i에 들어가는 수가 변경 문제의 크기
dp[i][j] => i와 j가 모두 변수임
```

## 문제풀이 꿀팁
> `i번째에 가능한 경우가 2가지 뿐이라면 2차원 다이나믹 말고 1차원 다이나믹으로 가능` => 이친수, 포도주 시식문제<br/>

> `(1)점화식 정의 무엇을 구할 것인가?`

<pre>
  <code>
    dp[i] = something i 번째 
    
    dp[i][j] => something i 번째의 j경우 등등
  </code>
</pre>
   
> `(2) 문제 쪼개고 i와 i-1번째의 관계를 보면서 가능한 경우의 수를 보며 점화식을 세운다.`

<pre>
  <code>
i번째의 경우가 a면 i-1에는 b경우가 올 수 있겠구나를 보면 된다.
  </code>
</pre>

> `거꾸로 할 때`
<pre>
  <code>
_    _  이 둘 사이 관계에서 i+1에서 무엇이 올 수 있는가를 본다.
i   i+1

배열의 어딘가가 빠진다 
-> + <- 서로 거꾸로 진행하는 방법 고려해볼 것.

예시)  연속합 2 문제에서 연속되는 합을 구하는데 한 개의 수를 제거   
     dp[i-1](->방향의 최대) + rdp[i+1] (<-방향의 최대) 이러면 자연스레 seq[i]가 빠진 최대가 나오지.   
     
  </code>
</pre>




