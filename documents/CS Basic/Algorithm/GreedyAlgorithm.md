# 최적화 문제

특정 문제를 해결하는 여러가지 방법 중에 최적의 해법(비용의 최소 등)을 찾는 문제 (the problem of finding the best solution from all feasible solutions)

## Local Optimum

최적화 문제를 해결할 때에는 local optimum 에 빠지지 않고 global optimum을 찾도록 하는 것이 중요하다.

![https://upload.wikimedia.org/wikipedia/commons/a/a1/Polynomialdeg4.png](https://upload.wikimedia.org/wikipedia/commons/a/a1/Polynomialdeg4.png)

# 탐욕 알고리즘 (Greedy Algorithm)

> 탐욕 알고리즘은 최적해를 구하는 데에 사용되는 근사적인 방법으로, 여러 경우 중 하나를 결정해야 할 때마다 **그 순간에 최적이라고 생각되는 것을 선택**해 나가는 방식으로 진행하여 최종적인 해답에 도달한다. 순간마다 하는 선택은 그 순간에 대해 지역적으로는 최적이지만, 그 선택들을 계속 수집하여 최종적(전역적)인 해답을 만들었다고 해서, 그것이 최적이라는 보장은 없다. 하지만 탐욕알고리즘을 적용할 수 있는 문제들은 지역적으로 최적이면서 전역적으로 최적인 문제들이다   - wikipedia

즉, 미래를 생각하지 않고 현재 가장 좋아보이는 선택을 하는 알고리즘.

- 장점: 빠른 계산 속도. 전체 문제를 보는 것이 아니라 문제의 부분만을 보고 결정하기 때문
- 단점: 알고리즘의 결과가 최적해(global optima)라는 것을 보장할 수 없다.

![https://miro.medium.com/max/1400/1*h8qoUKRVILm9vESQ6ZPj8A.png](https://miro.medium.com/max/1400/1*h8qoUKRVILm9vESQ6ZPj8A.png)

# 언제 사용하는가

탐욕 알고리즘이 잘 동작하기 위해서는 문제가 다음과 같은 특성을 가지고 있어야 한다.

- 탐욕스런 선택 속성(Greedy choice property)

    앞에서 선택한 것의 결과가 이후의 선택에 영향을 주지 않아야 한다.

- 최적 부분 구조(Optimal substructure)

    문제에 대한 최적해(Global optima)가 부분 문제에 대해서도 최적해가 된다.

위 두 가지 조건을 만족하지 못 한다면 탐욕 알고리즘은 최적해를 구하지 못 할 수 있다. 다만 근사해를 구하기 위해서 탐욕 알고리즘을 사용할 수 있다. (대부분의 경우 탐욕 알고리즘은 속도가 빠르고 어느정도 

[https://w.namu.la/s/f6f9d5e08e9beb596a8d52cdded15bbf5cf921aad3cd579360d23c8a578cd638099c8ce0ae12a11b63b85e68acc8fca2700172d5a45a9d87da2e006996865fe9d9b1075e20c9f0073e287f46937c747bef24a81564436821f5d62fcc526af992e3d9f5b7923c7a71b5b566cbf36b5c46](https://w.namu.la/s/f6f9d5e08e9beb596a8d52cdded15bbf5cf921aad3cd579360d23c8a578cd638099c8ce0ae12a11b63b85e68acc8fca2700172d5a45a9d87da2e006996865fe9d9b1075e20c9f0073e287f46937c747bef24a81564436821f5d62fcc526af992e3d9f5b7923c7a71b5b566cbf36b5c46)

# 오해

탐욕 알고리즘은 쉽다.

결론부터 말하면 쉽지 않은 알고리즘이다. 알고리즘 문제나 대회 등에서 탐욕 알고리즘을 가장 마지막에 고려하는 이유는 이 알고리즘의 결과가 최적해(global optima)라는 것을 증명하기가 어렵기 때문이다. 알고리즘의 결과가 최적임을 증명하는 것을 정당성 증명 이라고 하는데 탐욕 알고리즘의 결과는 항상 최적해를 보장하지 않기 때문에 정당성 증명을 해야한다. 

# 예시

대표적인 탐욕 알고리즘으로 다익스트라 알고리즘(Dijkstra Algorithm) 이 있다.


# 문제

## 동전 교환 문제(Coin Exchange Problem)

10원, 50원, 100원, 500원, 1000원이 있을 때, 2,750원를 교환할 수 있는 최소 동전 개수를 구하라.

## 회의실 배정

회사에 회의실이 하나밖에 없는데, n(<=100)의 팀이 각각 회의하고 싶은 시간을 다음 그림과 같이 제출했다고 한다. 두 팀이 동시에 회의실을 같이 쓸 수 없는 경우 최대로 많은 회의를 진행할 수 있는 최적해를 구하시오.([링크](https://algospot.com/judge/problem/read/MEETINGROOM))

---

참고. "탐욕 알고리즘", wikipedia

참고. 박상길. "파이썬 알고리즘 인터뷰"

참고. "최적화 문제", wikipedia

참고. "local optimum", wikipedia
