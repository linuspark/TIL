# 정렬(Sort) 알고리즘

정렬(Sort)은 주로 탐색(Search)를 위해 행해진다. 널리 사용되는 정렬 알고리즘을 이해하는 것은 CS의 다양한 알고리즘의 개념을 이해하는데 적당하다.

정렬 알고리즘은 정말 다양한 알고리즘이 존재하며 각 알고리즘의 동작 방식과 장단점을 이해하고 있으면 문제를 풀 때 어떠한 방법의 알고리즘을 이용하면 좋을지 판단할 수 있다.

[https://youtu.be/kPRA0W1kECg](https://youtu.be/kPRA0W1kECg)

# 버블 정렬(Bubble Sort)

- 실행 시간: $O(N^2)$
- 사용 메모리: $O(1)$

첫 원소와 그 다음 원소를 비교하여 현재 원소가 다음 원소보다 크다면 자리를 바꾼다. 이런식으로 모든 배열의 계속해서 살펴보고 완전히 정렬될 때 까지 반복한다.

```python
def bubbleSort(x):
	length = len(x)-1
	for i in range(length):
		for j in range(length-i):
			if x[j] > x[j+1]:
				x[j], x[j+1] = x[j+1], x[j]
	return x
```

![https://upload.wikimedia.org/wikipedia/commons/3/37/Bubble_sort_animation.gif](https://upload.wikimedia.org/wikipedia/commons/3/37/Bubble_sort_animation.gif)

# 선택 정렬 (Selection Sort)

- 실행 시간: $O(N^2)$
- 사용 메모리: $O(1)$

가장 간단하고 심플한 알고리즘이며 비효율적인 알고리즘이다. 원소의 배열 중 가장 작은 값을 찾아 배열의 맨 앞으로 가져온다. 이 후 두 번째로 작은 값을 찾아 배열의 두 번째 위치로 가져온다. 이런식으로 모든 원소가 정렬될 때 까지 반복한다.

```python
def selectionSort(x):
	length = len(x)
	for i in range(length-1):
	    indexMin = i
		for j in range(i+1, length):
			if x[indexMin] > x[j]:
				indexMin = j
		x[i], x[indexMin] = x[indexMin], x[i]
	return x
```

![https://upload.wikimedia.org/wikipedia/commons/b/b0/Selection_sort_animation.gif](https://upload.wikimedia.org/wikipedia/commons/b/b0/Selection_sort_animation.gif)


---

참고. 게일 라크만 맥도웰. 코딩 인터뷰 완전분석 (이창현 옮김)

참고. "거품 정렬", Wikipedia

참고. "선택 정렬", Wikipedia
