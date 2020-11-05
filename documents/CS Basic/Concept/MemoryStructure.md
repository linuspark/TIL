# 프로그램 실행 순서

프로그램이 실행되는 과정은 다음과 같다.

1. 사용자가 OS에 프로그램의 실행을 요청한다.
2. OS는 보조기억장치(HDD/SSD 등) 에서 프로그램을 읽어 주기억장치(메모리:RAM)에 올린다.
3. CPU는 메모리에 올라온 프로그램 코드를 이용하여 메모리를 관리하고 명령문을 실행한다.

# 메모리 구조

프로그램이 메모리에 올라올 때에는 그림과 같은 구조로 메모리에 데이터가 할당된다.

코드 영역과 데이터 영역은 컴파일 시점에 그 크기가 결정이 되고 스택 영역과 힙 영역은 런 타임에 크기가 결정된다. 또한 일반적으로 사용할 수 있는 메모리 주소가 한정되어 있기 때문에 스택 영역과 힙 영역이 서로 오버플로우가 발생할 수 있다.

![http://tcpschool.com/lectures/img_c_memory_structure.png](http://tcpschool.com/lectures/img_c_memory_structure.png)

## 코드 영역

프로그램의 실행할 코드(기계어) 가 저장된 부분으로 텍스트 영역 이라고도 불린다. CPU 는 이 부분에 저장된 명령어를 차례로 실행하게 된다. 이미 컴파일 될 때 고정되어 작성된 부분으로 읽기만 가능하다.

## 데이터 영역

프로그램의 전역 변수, 정적(static)변수가 저장되는 공간.

프로그램이 시작 될 때 할당되며 프로그램이 종료될 때 해제가 된다.

## 힙 영역

힙(Heap)은 사용자가 직접 관리하는 메모리 영역으로 동적으로 할당되고 해제되는 데이터가 저장되는 공간이다. 

C#이나 JAVA등의 고수준 언어에서는 가비지 컬랙터(Garbage Collector)가 주로 메모리를 해제한다. 클래스, 객체 등이 이 부분에 할당되며 런타임에 그 크기가 계속해서 변한다. 메모리 주소의 낮은 주소부터 높은 주소 방향으로 할당된다.

메모리의 주소값을 통해서 참조되고 사용된다.

## 스택 영역

프로그램이 자동으로 사용하는 메모리 영역이다. 지역변수, 매개변수, 리턴 값 등 임시로 사용되고 사라지는 데이터를 저장하기 위해 존재하는 공간이다.

메모리의 높은 주소부터 시작하여 낮은 주소 방향으로 할당되며 주로 메모리의 마지막 번지에서 시작한다.

# C# 에서 스택과 힙 메모리

C#에서 데이터가 스택 메모리나 힙 메모리에 저장되는 기준은 값 형식 데이터 인지, 참조 형식 데이터 인지에 따라 구분된다. 

- 값 형식 (Value Type) : 값을 변수에 직접 저장한다.
    - C# 에서는 정수, 부동소수점 숫자, 문자, bool, 구조체(struct), 열거형(enum), 값 튜플 등이 속한다.
- 참조 형식 (Reference Type) : 변수가 저장된 주소값(메모리 위치)을 저장하는 방식
    - C# 에서는 클래스, 인터페이스 등이 속한다.

값 형식을 변수에 저장하면 변수의 값은 스택 메모리에 저장된다.

```csharp
public void func(){
	int a = 10;
	float b = 0.1;
	a = 30;
	b = 4.5;
}
```

위와 같은 함수의 경우 함수가 시작되면서 해당 함수를 위한 공간이 스택 메모리에 할당이 되고 a 변수 위치에 10 이라는 값이, b 라는 위치에 0.1 이라는 값이 할당된다. 이 후 a 와 b 의 값이 변경될 때에는 기존에 저장되었던 스택 메모리 위치에 10 → 30, 0.1 → 4.5 이 되도록 값이 변경된다.

이 후 함수가 종료되어 나올 때 메모리에 할당되어 있던 데이터는 모두 해제된다.

참조 형식의 변수를 저장하는 경우에는 힙 메모리에 저장된다.

```csharp
public void Main(){
	var reference = new Reference(10);
	reference.internal_value = 30;

	var another = reference;
	another.internal_value = 40;
}
```

참조 형식으로 Reference라는 클래스의 인스턴스를 생성하고 초기 값을 10으로 설정하였다. var reference 부분이 실행 될 때 힙 메모리에는 Reference(10) 의 공간을 생성하고 해당 공간에 10을 저장한다. 

Main함수를 위한 스택 공간에는 reference 변수를 위한 공간이 생기고 해당 공간에는 힙 공간에 생성된 Reference(10)이 저장된 위치를 가리키는 값이 저장된다. 이 후 internal_value라는 값을 변경하게 되면 힙 공간에 있는 10이라는 값을 30으로 변경한다.

var another 에서는 동일한 힙 공간을 가리키는 변수를 스택 공간에 하나 더 생성하게 된다. another.internal_value를 변경할 때에도 힙 공간의 값을 변경하기 때문에 reference의 값도 변경되게 된다.

여기서 중요한 점은 스택 메모리에는 힙 메모리의 주소에 대한 정보가 저장된다는 점, 힙 메모리에는 실질적인 값이 저장된다는 점, 새로운 객체에 기존 변수를 할당하거나 함수의 인자로 넘길 때에는 스택 공간에 있는 주소값을 복사해 넘긴다는 점 등이 있다. 

힙 공간에 생성된 변수는 가비지 컬렉터에 의해 자동적으로 할당이 해제된다. 

---

참고. [http://tcpschool.com/c/c_memory_structure](http://tcpschool.com/c/c_memory_structure)

참고. [https://guslabview.tistory.com/186](https://guslabview.tistory.com/186)

참고. [https://docs.microsoft.com/ko-kr/dotnet/csharp/language-reference/builtin-types/value-types](https://docs.microsoft.com/ko-kr/dotnet/csharp/language-reference/builtin-types/value-types)
