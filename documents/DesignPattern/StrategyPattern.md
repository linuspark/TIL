# Strategy Pattern

전략 패턴, 스트레터지 패턴은 실행 중에 알고리즘을 선택할 수 있게 하는 "행위" 소프트웨어 디자인 패턴이다. "[템플릿 메소드 패턴](https://www.notion.so/Template-Method-Pattern-5b811ce90e0f4d609e45b113710e3739)" 과 마찬가지로 구체적인 내용과 일반적인 알고리즘을 분리하는 문제를 해결하기 위한 패턴이며 템플릿 메소트 패턴은 상속으로 문제를 해결하는 데 반해 스트레터지 패턴은 위임으로 문제를 해결한다.

OOP 에서 "상속" 이라는 개념은 아주 강력하지만 그만큼 비싼 대가를 치르기 때문에 상속으로 문제를 해결하기 보다 "위임"으로 문제를 해결하고자 하는 방법이다. 이 패턴도 의존 관계 역전 원칙을 따르기 위해 일반적인 알고리즘이 구체적인 구현에 의존하지 않도록 하며, 일반적인 알고리즘과 구체적인 구현은 추상화에 의존하도록 한다.

스트레터지 패턴은 다음과 같이 구성된다

![https://upload.wikimedia.org/wikipedia/commons/3/39/Strategy_Pattern_in_UML.png](https://upload.wikimedia.org/wikipedia/commons/3/39/Strategy_Pattern_in_UML.png)

- 특정 계열의 알고리즘(Strategy)을 정의하고
- 각 알고리즘을 캡슐화 하여 (interface)
- 이 알고리즘들(ConcreteStrategeA, ConcreteStrategyB)을 해당 계열 안에서 상호 교체가 가능하게 만든다

# Example: Bubble Sort

"[템플릿 메소드 패턴](https://www.notion.so/Template-Method-Pattern-5b811ce90e0f4d609e45b113710e3739)" 에서 사용했던 예제를 동일하게 사용해 본다.

```csharp
public class BubbleSorter {
	static int operations = 0;
	public static int sort(int[] array) {
		operation = 0;
		if (array.length <= 1)
			return operations;
			
		for (int nextToLast = array.length - 2; nextToLast >= 0; nextToLast--){
			for (int index = 0; index <= nextToLast; index++){
				compareAndSwap(array, index);
			}
		}
			
		return operations;
	}

	private static void swap(int[] array, int index) {
		int temp = array[index];
		array[index] = array[index+1];
		array[index+1] = temp;
	}

	private static void compareAndSwap(int[] array, int index) {
		if (array[index] > array[index + 1])
			swap(array, index);
		operations++;
	}
}
```

Int Array를 받아서 버블 정렬을 수행하는 클래스있다. 이 클래스를 리팩토링 하여 Int Array 뿐만 아니라 Double Array를 정렬할 수 있게 하려 한다.

그렇게 하기 위하여 일반적인 알고리즘인 Sort 부분과 구체적인 구현인 Array의 배열을 바꾸는 부분(Swap, CompareAndSwap)을 분리하여야 한다.

```csharp
public class BubbleSorter {
	private int operations = 0;
	private int length = 0; 
	private SortHandle itsSortHandle = null;

	public BubbleSorter(SortHandle handle) {
		this.itsSortHandle = handle;
	}

	public int sort(Object array) {
		this.itsSortHandle.setArray(array);
		this.length = this.itsSortHandle.length();
		operations = 0;
		if (this.length <= 1)
			return operations;

		for (int nextToLast = length - 2; nextToLast >= 0; nextToLast--){
			for (int index = 0; index <= nextToLast; index++) {
				if (itsSortHandle.outOfOrder(index))
					itsSortHandle.swap(index);
				operations++;
			}
		}
		return operations;
	}
}

public interface SortHandle {
	public void swap(int index);
	public bool outOfOrder(int index);
	public int length();
	public void setArray(Object array);
}

public class IntSortHandle: SortHandle{
	private int[] array = null;
		
	public void swap(int index){
		int temp = array[index];
		array[index] = array[index + 1];
		array[index + 1] = temp;
	}

	public void setArray(Object array){
		this.array = (int[]) array;
	}
	
	public int length(){
		return this.array.length;
	}

	public void outOfOrder(int index){
		return (array[index] > array[index + 1]);
	}
}
```

IntSortHandle은 Sort 알고리즘에 대해서, 즉 BubbleSorter에 대해서 아무런 의존성이 없다. 구체적인 구현(IntSortHandle)이 추상화(SortHandle)에만 의존하고 있는 것이다. 또 BubbleSorter는 IntSortHandle에 대하여 의존하지 않는다. 이로써 의존 관계 역전 원칙(DIP)을 지킬 수 있다.

사실 "[템플릿 메소드 패턴](https://www.notion.so/Template-Method-Pattern-5b811ce90e0f4d609e45b113710e3739)" 에서 해결했던 방식은 의존 관계 역전 원칙을 완전히 지키지는 않는다. 구체적인 구현인 IntBubbleSorter의 swap과 outOfOrder의 부분이 버블정렬 알고리즘에 직접 의존하고 있기 때문이다. 반면 스트레터지 패턴의 IntSortHandle은 버블 정렬 알고리즘에 직접적으로 의존하고 있지 않으며 다른 정렬의 알고리즘(퀵 정렬 등)에도 사용될 수 있다.

# 결론

위 예시에서 본 것과 같이 "스트레터지 패턴"은 "[템플릿 메소드 패턴](https://www.notion.so/Template-Method-Pattern-5b811ce90e0f4d609e45b113710e3739)" 에 비해 DIP를 완전히 지킬 수 있다는 이점을 제공한다. 즉, [템플릿 메소드 패턴](https://www.notion.so/Template-Method-Pattern-5b811ce90e0f4d609e45b113710e3739)은 일반적인 알고리즘으로 많은 구체적인 구현을 조작할 수 있게 하는 반면 스트레터지 패턴은 각각의 구체적인 구현이 더 많은 일반적인 알고리즘에 의해 조작될 수 있게 해준다. 

다만 두 패턴 모두 상위 단계의 알고리즘을 하위 단계의 구체적인 부분과 분리시키고 재 사용 가능하게 한 다는 점에서 같은 문제를 해결하고 있고 각각의 상황에 따라 알맞게 적용해야 한다. 일반적으로 스트레터지 패턴이 약간 더 복잡하고 메모리와 실행시간을 더 잡아먹으며 알고리즘과 구제적인 구현 부분을 독립적으로 재사용되게 할 수 있다.

---

참고. 로버트C마틴. 클린 소프트웨어 애자일 원칙과 패턴 그리고 실천 방법 (이용원, 김정민, 정지호 옮김) 

참고. "전략패턴", Wikipedia