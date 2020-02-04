# Dynamic Programming

### Introdution

`큰 문제를 작은 문제로 나눠서 푸는 알고리즘`

> `<< DP와 분할정복의 차이 >>`
>   >1. 다이나믹 프로그래밍 - 문제를 나눠도 문제의 크기가 중복될 수있음
>   >2. 분할 정복 - 문제를 나누면 이전에 나왔던 문제의 크기가 중복될 수 없음

### Condition

`이 문제가 다이나믹 프로그래밍기법으로 해결이 가능한가?`

<< 다음의 2가지 조건을 만족 >>
>1. Overlapping Subprobelm(겹치는 부분문제)
>   >중복되는 부분(작은)문제들로 큰 문제를 나눌수 있다.
>2. Optimal Substructure(최적 부분구조)
>   >작은문제들의 정답으로 큰 문제의 정답을 도출할 수 있어야 한다.
>예시
>   >피보나치 수열

