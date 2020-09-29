# Null Object Pattern

OOP 에서 null 객체는 참조 값을 가지고 있지 않거나 아무런 행동이 정의되어 있지 않은 것을 의미한다. 널 오브젝트 패턴(Null Object Pattern)은 이런 Null 객체를 모사하는 객체를 만듦으로써 아무것도 정의되지 않은 상황을 구현하는 패턴이다. 즉, Null의 행위를 정의한 객체를 만들어 사용하는 패턴이라고 할 수 있다.

## Motivation

대부분의 객체 지향 언어에는 Null이 존재하며 객체가 Null을 참조하고 있는지 검사하는 것은 꽤 중요하다. null을 참조하고 있다면 해당 객체에서는 함수를 호출하거나 다른 맴버변수를 참조할 수 없기 때문에 런타임 오류가 발생할 수 있기 때문이다.

```csharp
Employee e = DB.getEmployee("Bob");
if (e != null && e.isTimeToPay(today))
	e.pay()
```

주로 위와 같은 방식으로 객체가 null인지 확인하고 null이 아닌 경우 다음 액션을 수행한다. 이런 방법은 흔한 방법이지만 null 체크를 잊어버리는 실수를 하기 쉽고 코드가 보기에도 좋지 않아 보인다.

클린코드에 따르면 null을 반환하는 함수는 지양하도록 되어 있으며 null을 반환하지 않기 위해 에러를 던질 수도 있다. 위 getEmployee 함수에서 Employee가 없는 경우 에러를 던지도록 구성하였다면 getEmployee함수 호출 블록을 try-catch로 감싸주어야 할 것이다. 이런 방식도 별로 보기 좋은 방법은 아닌 듯 하다.

## Null Object Structure

널 오브젝트 패턴을 이용하여 위 문제를 해결하면 다음과 같은 방식으로 해결할 수 있다.

[http://www.plantuml.com/plantuml/svg/SoWkIImgAStDuKhEIImkLd1nuihCAqajIajCJbLmpIt8oQzCJONA-PNcvA09mRYUG3epDpMl9B4aCp-FYyl5IK7N3g4VMQU2Rcc1RWsI97Opq9L1ZKGnoKh1niQvA3Mn9DNE3YgFtJ1KbGwfUIb07mC0](http://www.plantuml.com/plantuml/svg/SoWkIImgAStDuKhEIImkLd1nuihCAqajIajCJbLmpIt8oQzCJONA-PNcvA09mRYUG3epDpMl9B4aCp-FYyl5IK7N3g4VMQU2Rcc1RWsI97Opq9L1ZKGnoKh1niQvA3Mn9DNE3YgFtJ1KbGwfUIb07mC0)

NullEmployee 객체는 모든 메소드가 "아무 일"도 하지 않는다. 여기서 "아무 일" 이란 우리가 Null 객체에게 원하는 행동이 될 수 있다. DB의 getEmployee 매소드는 Employee를 찾지 못 하였을 때 NullEmployee를 반환한다.

위 방식을 이용하면 다음과 같이 코드를 작성할 수 있다.

```csharp
Employee e = DB.getEmployee("Bob");
if (e.isTimeToPay(today))
	e.pay()
```

이 때 getEmployee함수가 NullEmployee를 반환하였다면 NullEmployee의 isTimeToPay() 함수의 동작은 false를 반환하는 것이 우리가 NullEmployee에게 바라는 행위일 것 이다.

# 결론

널 오브젝트 패턴은 기본적으로 Null Check 를 해야 한다는 생각을 바꾸어준다. null이나 0을 반환하는 함수는 오류를 만들기 쉽고 만들어 낸 오류를 찾아내기도 어렵다. 함수가 실패한 경우에도 항상 유요한 객체를 반환하며 실패를 나타내는 객체들은 '아무일'도 하지 않는다.
