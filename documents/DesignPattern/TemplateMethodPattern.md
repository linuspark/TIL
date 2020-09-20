# Template Method Pattern

객체 지향 프로그래밍 에서 중요한 "상속" 이라는 개념은 **차이에 의한 프로그래밍**을 가능하게 한다. 즉 어떤 중요한 일을 수행하는 클래스가 이미 있다면 그 클래스를 상속받아 일부분만 수정함으로써 새로운 기능을 하는 프로그램을 만들 수 있는 것이다.

템플릿 메소드 패턴은 **행위/행동을 디자인 하는 패턴**으로, 알고리즘의 프로그램 뼈대를 정의하는 패턴이다. 알고리즘의 구조는 변경하지 않고 알고리즘의 특정 단계를 다시 정의할 수 있게 한다. 

구체적인 내용으로 부터 일반적인 알고리즘을 분리하는 문제를 해결하는 패턴으로 "스트레티지 패턴"과 호환되어 사용된다. (스트레티지 패턴은 위임으로, 탬플릿 메소드 패턴은 상속으로 문제를 해결한다.)

의존 관계 역전을 위하여 일반적인 알고리즘이 구체적인 구현에 의존하지 않도록 하고, 일반적인 알고리즘과 구체적인 구현이 추상화에 의존하도록 한다.

# Example: Bubble Sort

문제.

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

위 BubbleSorter 클래스는 int array을 입력으로 받아서 버블 정렬을 수행하는 클래스 이다. 위 클래스를 분석해 보면 sort 라는 함수는 알고리즘을 가지고 있고, swap과 compareAndSwap이라는 함수는 sort라는 함수의 보조 함수로 int 형 배열을 직접 처리하는 구체적인 부분이다. 

이제 int 형이 아닌 double 형의 array를 입력으로 받아 버블 정렬을 수행하는 클래스를 만들기 위해 탬플릿 메소드를 이용하여 리팩토링 하면 아래와 같이 될 수 있다.

```csharp
public abstract class BubbleSorter {
	private int operations = 0;
	protected int length = 0;
	
	protected int doSort() {
		operations = 0;
		if (length <= 1)
			return operations;
	
		for (int nextToLast = length - 2; nextToLast >= 0; nextToLast--){
			for (int index = 0; index <= nextToLast; index++){
				if (outOfOrder(index))
					swap(index);
				operations++;
			}
		}

		return operations;
	}

	protected abstract void swap(int index);
	protected abstract bool outOfOrder(int index);	
}

public class IntBubbleSorter: BubbleSorter {
	private int[] array = null;

	public int sort(int[] intArray) {
		array = intArray;
		length = array.length;
		return doSort();
	}

	protected void swap(int index) {
		int temp = array[index];
		array[index] = array[index + 1];
		array[index + 1] = temp;
	}

	protected bool outOfOrder(int index) {
		return (array[index] > array[index + 1]);
	}
}

public class DoubleBubbleSorter: BubbleSorter {
	private double[] array = null;

	public int sort(double[] doubleArray) {
		array = doubleArray;
		length = array.length;
		return doSort();
	}

	protected void swap(int index) {
		double temp = array[index];
		array[index] = array[index + 1];
		array[index + 1] = temp;
	}

	protected bool outOfOrder(int index) {
		return (array[index] > array[index + 1]);
	}
}
```

일반적인 알고리즘은 기반 클래스(abstract class)에 있고, 다른 구체적인 내용은 상속되어 구현된다. 

# 결론

탬플릿 메소드는 상위 단계의 알고리즘을 하위 단계의 구체젹인 부분으로 부터 분리 하도록 하여 상위 알고리즘이 구체적인 부분과 독립적으로 재 사용될 수 있게 한다. 

---

참고. 로버트C마틴. 클린 소프트웨어 애자일 원칙과 패턴 그리고 실천 방법 (이용원, 김정민, 정지호 옮김) 

참고. "템플릿 메소드 패턴", Wikipedia
