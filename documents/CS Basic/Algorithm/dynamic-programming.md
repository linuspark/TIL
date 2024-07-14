# 동적 프로그래밍(Dynamic Programming)

> 수학과 컴퓨터 과학, 그리고 경제학에서 동적 계획법(動的計劃法, dynamic programming)이란 복잡한 문제를 간단한 여러 개의 문제로 나누어 푸는 방법을 말한다. 이것은 부분 문제 반복과 최적 부분 구조를 가지고 있는 알고리즘을 일반적인 방법에 비해 더욱 적은 시간 내에 풀 때 사용한다.  -wikipedia

동적 프로그래밍은 거의 대부분이 재귀와 부분 문제(sub-problem)을 찾은 뒤에 나중을 위해 현재 결과를 저장해 놓는 방식으로 문제를 해결한다. 즉, 동적 프로그래밍은 문제를 여러 부분 문제로 나누어 푼 다음 그것을 결합하여 최종 결과를 계산해 내는데, 이 때 각 하위 부분 문제의 결과를 저장해 두었다가 나중에 같은 문제가 나왔을 경우 저장해 놓은 결과를 사용하여 간단하게 문제를 해결하는 방법이다. → **"답을 재활용 하는 것"**

간혹, 하향식 동적 프로그래밍을 "메모이제이션" 이라고 하고 상향식 동적 프로그래밍 만을 "동적 프로그래밍"이라고 구분하여 부르기도 하지만 여기서는 모두 "동적 프로그래밍"이라고 한다.

# 예시

피보나치 수열

동적 프로그래밍을 이해하기 위한 가장 대표적인 예시로 피보나치 수열을 이야기 한다.

1. 재귀로 구현하기

    ```python
    def fibonacci(n):
        if n is 0 or n is 1:
            return n
        return fibonacci(n-1) + fibonacci(n-2)
    ```

    재귀로 구현한 피보나치 함수의 시간복잡도는 $O(2^N)$ 이 된다. 말단노드에 도달하기 까지 매 번 2개의 자식노드를 생성하고 있고 각 함수의 호출에는 O(1)의 시간이 소요되기 때문이다. 정확히 하면 $O(2^N)$ 보다는 조금 빠른 정도이다.

    [https://w.namu.la/s/9ed9e9ddd2b5cc0453ab51b3052f1e799fe2f33c60d877f2de75ac213796584f87f1e490829f655561986fcf4f68a8bae9fa20726b416f1b2980379032f30b3a29c8edd8c4028e387c621ef8bfa972b80ed15d9b0233c35ba3fbd54c93517ea139cb1085f2dd1fd059aba2204a5e6867](https://w.namu.la/s/9ed9e9ddd2b5cc0453ab51b3052f1e799fe2f33c60d877f2de75ac213796584f87f1e490829f655561986fcf4f68a8bae9fa20726b416f1b2980379032f30b3a29c8edd8c4028e387c621ef8bfa972b80ed15d9b0233c35ba3fbd54c93517ea139cb1085f2dd1fd059aba2204a5e6867)

    N의 숫자가 작을 때에는 별 문제가 되지 않지만 N의 숫자가 커질 수록 소요시간이 기하급수적으로 증가하게 된다.

2. 하향식 동적 프로그래밍(메모이제이션)

    재귀 트리를 보면 중복되는 계산이 꽤나 많이 존재함을 볼 수 있다. fib(3)의 경우 2번 호출, fib(2)의 경우 3번 호출 되었다. 이 함수들은 사실 한 번 계산되면 그 값을 중복해서 사용해도 될 것이다.

    사실 fib(N)를 계산하고자 할 때, fib 는 N 번만 호출하면 fib(N)을 계산할 수 있다. 매번 fib(i)를 호출할 때 그 값을 저장해 두고 나중에는 저장된 값을 사용하는 것이다.

    ```python
    def fibonacci(num):
        memo = dict()
        return fibonacci_memo(num, memo)

    def fibonacci_memo(num, memo):
        if num is 1 or num is 0:
            return num
        if num not in memo.keys():
            memo[num] = fibonacci_memo(num - 1, memo) + fibonacci_memo(num - 2, memo)
        return memo[num]
    ```

3. 상향식 동적 프로그래밍

    반대 방향으로 접근하여 문제를 풀 수도 있다. 초기 fib(0)과 fib(1)을 이용하여 N 까지 올라가면서 미리 계산해 놓은 답을 사용할 수도 있다.

    ```python
    def fibonacci(num):
        if num is 1 or num is 0:
            return num
        memo = dict()
        memo[0] = 0
        memo[1] = 1
        for i in range(2, num):
            memo[i] = memo[i-1] + memo[i-2]
        return memo[num-1] + memo[num-2]
    ```

    위 예시에서 memo[i]는 사실 memo[i+1]과 memo[i+2]를 계산할 때에만 사용된다. 이런 점을 생각하면 공간복잡도를 조금 더 줄일 수 있을 것이다.

# 문제

### 트리플 스텝

어떤 아이가 n개의 계단을 오른다. 한번에 1개의 계단을 오르거나 2개의 계단, 3개의 계단을 오른다. 계단을 오르는 방법이 몇 가지가 있는지 계산하는 매서드를 구현하라

### 격자판(grid)상의 로봇

행의 개수는 r, 열의 개수는 c 인 격자판의 왼쪽 상단 꼭지점에 로봇이 놓여있다. 이 로봇은 오른쪽 아래로만 이동할 수 있다. 하지만 어떤 셀(cell)은 '금지 구역' 으로 정의되어 로봇이 접근 할 수 없다. 왼쪽 상단 꼭지점에서 오른쪽 하단 꼭지점으로 경로를 찾는 알고리즘을 설계하여라

```csharp
public List<Point> GetPath(bool[][] maze){
}
```

### 여덟 개의 퀸

8x8 체스판 위에 여덟 개의 퀸(Queen)이 서로 잡아 먹히지 않도록 놓을 수 있는 모든 가능한 방법을 출력하는 알고리즘을 작성하라. 즉, 퀸은 서로 같은 행, 열, 대각선상에 놓이면 안된다.

---

참고. 게일 라크만 맥도웰. 코딩 인터뷰 완전분석 (이창현 옮김)

참고. "동적 계획법", Wikipedia

참고. <파이썬 알고리즘 인터뷰> p.628, 책만, 2020