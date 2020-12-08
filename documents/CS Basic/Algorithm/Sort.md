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

# 병합 정렬 (Merge Sort)

- 실행 시간: $O(NlogN)$
- 사용 메모리: 가변

배열을 절반으로 나누어 각각 정렬한 다음 둘을 하나로 합하여 다시 정렬하는 방법. 나눈 절반을 정렬할 때에도 같은 방법을 사용하는 전형적인 분할-정복 알고리즘(Divide and conquer algorithm)이다. 이 알고리즘은 "병합"  을 처리하는 부분이 가장 복잡하다. 

병합은 합치고자 하는 두 배열의 시작 지점에서 차례로 읽으면서 더 작은 원소를 꺼내와 새로운 배열을 만드는 방식으로 진행된다. 

![https://upload.wikimedia.org/wikipedia/commons/c/cc/Merge-sort-example-300px.gif](https://upload.wikimedia.org/wikipedia/commons/c/cc/Merge-sort-example-300px.gif)

```python
def mergesort(x):
	if len(x) <= 1:
		return x
	mid = len(x) // 2
	left = x[:mid]
	right = x[mid:]
	left = mergesort(left)
	right = mergesort(right)
	return merge(left, right)

def merge(a, b):
	result = list()
	while len(a) > 0 or len(b) > 0:
		if len(a) is 0:
			result += b
			break
		if len(b) is 0:
			result += a
			break
		if a[0] > b[0]:
			result.append(b[0])
			b = b[1:]
		else:
			result.append(a[0])
			a = a[1:]
	return result
```

# 퀵 정렬 (Quick Sort)

- 실행 시간: $O(NlogN)$ / 최악의 경우 $O(N^2)$
- 사용 메모리: $O(logN)$

무작위로 한 원소(피벗:pivot)를 선택하여 해당 원소보다 작은 것은 그 원소 앞으로, 큰 것은 그 원소 뒤로 보낸다. 이제 피벗(pivot) 앞 부분의 배열과 뒷 부분의 배열을 각각 같은 방법으로 정렬한다. 

해당 배열과 부분 배열을 계속해서 분할하여 처리하다 보면 정렬이 완성되는 분할-정복 알고리즘의 하나이다. 이 알고리즘의 경우 피벗(pivot)이 어떻게 선택되느냐에 따라 최악의 수행시간이 N^2 이 될 수 있다. (피벗을 항상 최댓값이나 최솟값을 선택하는 경우, 예를 들어 이미 정렬된 배열에서 항상 피벗을 첫 번째 원소로 하는 경우)

![https://upload.wikimedia.org/wikipedia/commons/6/6a/Sorting_quicksort_anim.gif](https://upload.wikimedia.org/wikipedia/commons/6/6a/Sorting_quicksort_anim.gif)

```python
def quicksort(x):
    if len(x) <= 1:
        return x
    pivot = x[len(x) // 2]
    less = []
    more = []
    equal = []
    for a in x:
        if a < pivot:
            less.append(a)
        elif a > pivot:
            more.append(a)
        else:
            equal.append(a)
    return quicksort(less) + equal + quicksort(more)
```

퀵 정렬은 대부분의 컴퓨터 아키텍처에서 효율적으로 동작하도록 설계되어 있으며(지역성Locality) 매 정렬에서 적어도 1 개의 원소가 자기 위치(정렬된 위치) 를 찾아가기 때문에 다른 O(nlogn) 알고리즘 보다 빠르게 동작한다.

- 지역성 Locality: CPU가 짧은 시간 동안 기억 장치 내의 특정 메모리 영역에 반복적으로 엑세스 하는 경향. 즉, 짧은 시간 동안 특정 영역에 있는 데이터에 집중적으로 엑세스하는 경향을 말한다. 이 성질은 cache 를 이용하는 이유가 된다.

# 힙 정렬 (Heap Sort)

- 실행 시간: $O(NlogN)$
- 사용 메모리: $O(logN)$

최대 힙 혹은 최소 힙을 구성하여 정렬하는 방법. 

최대/최소 힙을 구성하는 데 $O(logN)$ 의 시간이 걸리고 해당 힙에서 N 개의 데이터를 뽑아내어(삭제) 데이터를 정렬하기 때문에 실행시간은 $O(NlogN)$ 이 걸린다.

![https://upload.wikimedia.org/wikipedia/commons/1/1b/Sorting_heapsort_anim.gif](https://upload.wikimedia.org/wikipedia/commons/1/1b/Sorting_heapsort_anim.gif)

---

참고. 게일 라크만 맥도웰. 코딩 인터뷰 완전분석 (이창현 옮김)

참고. "거품 정렬", Wikipedia

참고. "선택 정렬", Wikipedia

참고. "병합 정렬", Wikipedia

참고. "퀵 정렬", Wikipedia

참고. "힙 정렬", Wikipedia
