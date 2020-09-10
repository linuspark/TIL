

'빅 오 표기법' 이라고 하는 표기법은 알고리즘의 효율성을 나타내기 위하여 만들어진 표기법이다.

복잡도 라고 이야기 하기도 한다.

컴퓨터 과학에서 복잡도는 크게 시간 복잡도와 공간 복잡도를 이야기한다.

# 시간 복잡도

Big O 시간. 알고리즘이 수행되는 시간에 대하여 표기한 것. 자세히 따지면 최대 시간이냐 최소 시간이냐 평균 시간이냐에 따라서 Big-O / Big-theta / Big-Omega 등으로 나뉘어 지기는 하지만 보통은 수행시간을 딱 맞게 하는 시간을 의미한다.

시간 복잡도는 시간과 입력 데이터 개수의 관계를 표현한 것 이다. 예를 들어 N개의 데이터를 처리하는데 있어서 N개의 데이터를 한번씩 읽어 봐야 한다면 O(N) 이라고 표기할 수 있다. 마찬가지로 N개의 데이터를 처리하는데 항상 일정한 시간이 소요된다면 O(1) 이라고 표기한다. 같은 방법으로 O(N), O(log N), O(N log N), O($N^2$), O($2^N$) 등의 표기법이 있다.

## O(1)

```csharp
public int Algorithm(int[] dataArray){
	return dataArray[0]
}
```

입력으로 받은 데이터의 특정 원소에 직접 접근할 수 있고 입력 데이터의 크기와 함수를 수행하는 시간이 연관이 없는 경우

## O(N)

```csharp
public int SumOfArray(int[] dataArray){
	int sum = 0;
	for(i = 0; i < dataArray.Length; i++){
		sum += i;
	}
	return sum;
}
```

입력으로 받는 데이터의 크기에 따라서 함수의 수행 시간이 비례해서 커지는 경우

## O(N^2)

```csharp
public void printArrayMultiple(int[] dataArray){
	for(int i = 0; i < dataArray.Length; i++){
		for(int j = 0; j < dataArray.Length; j++){
			System.Console.println($"Data:{i * j}");
		}
	}
}
```

입력으로 받은 데이터 한 개당 입력으로 받은 데이터 전체를 순회해서 보아야 하는 경우

# 공간 복잡도

알고리즘에 대하여 분석을 할 때 시간에 대한 것 만큼 공간에 대한 것도 중요하다(최근 대용량 데이터를 처리할 수 있는 기술의 증가로 중요성이 떨어지기는 하였다.)

공간 복잡도는 시간 복잡도와 평행선을 이루는 개념이다. 크기가 N 인 배열을 만드는데 필요한 공간 복잡도는 O(N), N * N 크기의 2차원 배열을 만드는 데 필요한 공간 복잡도은 O($N^2$) 이다.

공간복잡도를 계산할 때에는 호출에 사용되는 스택공간도 공간복잡도 계산에 포함되어야 한다.

아래는 피보나치 수열을 구하는 함수에 대한 공간복잡도 예시이다.

```python
def fibonacci(num):
    if num < 2:
        return num
    return fibonacci(num - 1) + fibonacci(num - 2)

```

```python
def fibonacci(num):
    if num < 2:
        return num
    answer = 0
    f1 = 0
    f2 = 1
    for i in range(1, num):
        answer = f1 + f2
        f1 = f2
        f2 = answer

    return answer

```

위 두 코드는 각각 O(N), O(1) 의 공간복잡도를 가진다.

# 복잡도의 계산

시간/공간 복잡도는 기본적으로 입력으로 받는 인자의 개수에 따라 시간적, 공간적으로 얼마만큼의 자원이 필요하게 되는지 수학적으로 계산하여 나타내게 된다. 이 때 몇 가지 주의해야 할 점들이 있다.

## 상수의 무시

Big-O 표기법은 단순히 증가하는 비율을 나타내는 개념이다. 이 개념에서 상수의 존재는 의미가 없다.

때문에 Big-O 를 계산할 때에 상수는 무시하여 표기한다. O(N)이나 O(2N)이나 O(N+4) 이나 모두 O(N)으로 표기한다. Big-O 표기법은 알고리즘의 정확한 시간적/공간적 복잡성을 표기하기 위한 것이 아니라는 것에 주의해야 한다. O(N)이 O(2N)보다 언제나 나은 것은 아니며 O(N) 의 코드가 O(1) 의 코드보다 빠르게 동작할 수도 있는 법이다.

## 지배적이지 않은 항 무시

$O(N^2+N)$과 같은 수식의 경우 $O(N^2)$ 로 표기하여 지배적이지 않은 항은 무시한다. 이것 또한 상수항을 무시하는 이유와 같은 이유이다.

-   $O(N^2 + N)$은 $O(N^2)$ 가 된다.
-   $O(N + logN)$의 경우 $O(N)$이 된다.
-   $O(10*2^N + 1000 N^3)$의 경우 $O(2^N)$ 이 된다.

즉, 지배적인 항만 살아남는 것. 다만 그렇다고 수식에 합이 있으면 안되는 것은 아니다.

$O(A + B)$의 경우 하나의 항으로 줄일 수 없다. (A와 B 의 관계를 알고 있지 않은 이상 두 개의 다른 인자를 없앨 수는 없다.)

## 여러 부분으로 이루어진 알고리즘

위에서 예시를 보인 것 처럼 두 개의 인자가 알고리즘에 사용 되는 경우 계산 방식이 헷갈릴 수 있다. 어떤 경우에 더하고 어떤 경우에 곱해야 하는지 명확하게 이해하고 있어야 한다.

$O(A+B)$

```python
a = [1, 2, 3, 4]
b = ['a', 'b', 'c']

for i in a:
    print(i)

for i in b:
    print(i)


```

$O(A\times B)$

```python
a = [1, 2, 3, 4]
    b = ['a', 'b', 'c']

    for i in a:
        for j in b:
            print(f'{i}, {j}')

```

# 복잡도 계산의 패턴

## 복잡도의 종류

![https://upload.wikimedia.org/wikipedia/commons/thumb/7/7e/Comparison_computational_complexity.svg/1920px-Comparison_computational_complexity.svg.png](https://upload.wikimedia.org/wikipedia/commons/thumb/7/7e/Comparison_computational_complexity.svg/1920px-Comparison_computational_complexity.svg.png)

## O(log N)

이진 탐색(Binary Search) 의 경우를 예로 들어 시간 복잡도를 계산 해본다.

Q. N개의 정렬된 원소가 있는 배열에서 원소 X 를 이진 탐색으로 찾을 때 이 알고리즘의 시간복잡도는?

-   X 와 배열의 중간 값을 비교
    -   중간 값 == X : 반환
    -   중간 값 > X : 배열의 왼쪽 부분에서 재 탐색
    -   중간 값 < X : 배열의 오른쪽 부분에서 재 탐색

처음에는 N개의 배열 → N/2 의 배열 → N/4의 배열 → N/8의 배열 순서로 탐색하게 된다.

N/2 → N/4 → N/8 → ... → 1 와 같은 순서로 배열의 크기가 달라질 것이다. 이 때 몇 번(k 번)의 과정 끝에 1이 나오는 지를 찾는 문제가 된다. 이를 반대로 하면 1 → 1 *2 → ... → N/2 로 볼 수 있으며 몇 번(k 번) 수행했을 때 N을 만들 수 있을까. 수식으로 표현하면 $2^k = N$ 이 된다. 계산하면, $k = log_2N$ 으로 표현할 수 있다.

즉, 이진탐색의 시간 복잡도는 $O(log N)$이라고 할 수 있다.

여기서 로그 밑은 상수 취급되어 무시한다.

## 재귀함수의 수행 시간

피보나치 수열을 구하는 함수를 재귀함수로 구현하여 복잡도를 계산해 본다.

```python
def fibonacci(num):
    if num < 2:
        return num
    return fibonacci(num - 1) + fibonacci(num - 2)

```

위 코드의 경우 한 번 함수가 호출 될 때 마다 자기 자신을 2번 호출한다. 자기 자신을 호출하는 것을 멈추는 순간은 num의 값이 1 이하가 될 때이다. 단순하게 생각하면 호출 스택의 깊이는 총 N 이 될 것 이라는 것을 알 수 있다.

즉, $1 + 2^1 + 2^2 +..+2^N = 2^{N+1} -1$ 의 시간이 걸릴 것이고 이를 시간복잡도로 표현하면 $O(2^n)$이 된다.

즉, 시간 복잡도의 경우 $O(2^n)$이 된다.

또한 호출 스택의 깊이는 N 이고 특정 시간에 사용되는 메모리(공간)의 크기는 $O(N)$이 된다

즉, 공간 복잡도의 경우 $O(N)$이 된다.

---

참고. 게일 라크만 맥도웰. 코딩 인터뷰 완전분석 (이창현 옮김)

참고. "Big O Notation", Wikipedia