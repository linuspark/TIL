# 백 트래킹(퇴각검색:Backtracking)

> 백 트래킹은 해결책에 대한 후보를 구축해 나아가다 가능성이 없다고 판단되는 즉시 후보를 포기(백트랙Backtrack)해 정답을 찾아나가는 범용적인 알고리즘으로 제약 충족 문제(Constraint Satisfaction Problem) 에 특히 유용하다.

## 제약 충족 문제(Constraint Satisfaction Problem:CSP)

> 제약 충족 문제란 복수의 제약조건(Constraint)을 충족하는 상태를 찾아내는 문제를 뜻한다(ex. 스도쿠, 8-queen's problem)

대표적으로 스도쿠 처럼 1에서 9 까지의 숫자를 한 번만 넣는(제약 조건 충족) 정답(상태)을 찾아내는 모든 유형의 문제들을 의미한다. 보통 합리적인 시간 안에 문제를 풀이하기 위하여 휴리스틱과 조합 탐색 같은 개념을 결합하여 문제를 풀이한다.  

![https://upload.wikimedia.org/wikipedia/commons/thumb/8/8c/Sudoku_solved_by_bactracking.gif/220px-Sudoku_solved_by_bactracking.gif](https://upload.wikimedia.org/wikipedia/commons/thumb/8/8c/Sudoku_solved_by_bactracking.gif/220px-Sudoku_solved_by_bactracking.gif)

## 깊이 우선 탐색 (Depth First Search: DFS)

![https://upload.wikimedia.org/wikipedia/commons/thumb/2/2c/Depthfirst.png/250px-Depthfirst.png](https://upload.wikimedia.org/wikipedia/commons/thumb/2/2c/Depthfirst.png/250px-Depthfirst.png)

백 트래킹과 DFS는 항상 함께 이야기 된다. 백 트래킹이 조금 더 큰 의미를 가지며 백 트래킹은 DFS와 같은 방식으로 구현된 모든 탐색 방법을 의미한다. 즉, DFS는 백 트래킹의 골격을 이루는 알고리즘이라고 할 수 있다.

DFS가 그렇듯 백 트래킹도 주로 재귀를 이용하여 구현된다. 

백 트래킹은 가보고 되돌아오고를 반복하여 해법을 찾아내기 때문에 운이 좋은 경우 빠르게 해법을 찾을 수 있고 운이 나쁜 경우 모든 경우의 수를 검색해 본 뒤에 해법을 찾을 수도 있다.

얼핏 브루트포스와 유사하지만 한번 방문 시, 후보가 가능성이 없다면 빠르게 후보를 포기한다는 점에서 효율성이 있다.

## 가지치기(Pruning)

트리에서 불필요한 요소를 제거하여 탐색의 범위를 제한하는 것을 의미한다.

백 트래킹에서는 이 가지치기를 이용하여 탐색의 범위를 제한하고 브루트 포스 보다 빠르게 해법을 찾아낼 수 있다. 

![https://media.vlpt.us/images/prayme/post/65c5f8f4-1018-4201-b2a1-10532ee7dfbe/image.png](https://media.vlpt.us/images/prayme/post/65c5f8f4-1018-4201-b2a1-10532ee7dfbe/image.png)

브루트 포스로 모든 경우의 수를 탐색하는 경우.

![https://media.vlpt.us/images/prayme/post/9e06019c-5329-423d-afa9-6c517baa1832/image.png](https://media.vlpt.us/images/prayme/post/9e06019c-5329-423d-afa9-6c517baa1832/image.png)

가지치기를 하여 불필요한 부분을 일찍 포기한 경우.

---

참고. Wikipedia, [Constraint satisfaction problem](https://en.wikipedia.org/wiki/Constraint_satisfaction_problem)

참고. Wikipedia, [Backtracking](https://en.wikipedia.org/wiki/Backtracking)

참고. Wikipedia. [퇴각검색](https://ko.wikipedia.org/wiki/퇴각검색)

참고. 박상길, 파이썬 알고리즘 인터뷰,(책만)