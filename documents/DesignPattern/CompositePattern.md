# Composite Pattern

![https://upload.wikimedia.org/wikipedia/commons/thumb/5/5a/Composite_UML_class_diagram_%28fixed%29.svg/960px-Composite_UML_class_diagram_%28fixed%29.svg.png](https://upload.wikimedia.org/wikipedia/commons/thumb/5/5a/Composite_UML_class_diagram_%28fixed%29.svg/960px-Composite_UML_class_diagram_%28fixed%29.svg.png)

컴포지트 패턴(Composite pattern)이란 객체들의 관계를 트리 구조로 구성하여 부분-전체 계층을 표현하는 패턴으로, 사용자가 단일 객체와 복합 객체 모두 동일하게 다루도록 한다. - wikipedia

컴포지트 패턴은 아주 단순하지만 가지고 있는 의미는 크다. 위 다이어그램에서 Composite 클래스는 여러 Component 클래스를 가지고 있을 수 있고 하나의 Component (파생) 클래스로 동작할 수 있다. 즉, Composite클래스는 그냥 일반 Component 클래스 이며 하는 행위도 Component 클래스와 다를게 없어 보인다. 하지만 사실 Composite 클래스는 여러 Component 인스턴스 집합의 프록시이다. 

# 예시: 컴포지트 커맨드

아래는 커맨드패턴을 이용한 예제이다. 

UML

Sensor 객체는 특정 이벤트를 감지하면 Command 객체의 do() 함수를 실행한다. Sensor는 어떤 Command 객체가 오는지에 상관 없이 Command 객체가 가진 인터페이스 do()를 실행하는 것이다. 이렇게 구성된 시스템에서 Sensor 객체가 이벤트를 감지하였을 때 특정 N개의 Command 객체의 do()를 실행해야 하는 상황을 가정한다.

생각할 수 있는 간단한 방법으로는 Sensor가 Command 객체의 리스트를 가지고 있고 이벤트가 발생하였을 때 Command 객체의 리스트를 순회하면서 do() 함수를 실행하는 것을 생각 할 수 있다.

UML

이런 상황에서 컴포지트 패턴을 사용하게 되면 깔끔하고 간단하게 해결할 수 있다.

UML 

Sensor 나 Command 객체를 수정하지 않고 Composite Command 라는 새로운 클래스를 생성함으로써 문제를 해결하였다. 이런 방식은 OCP를 만족시킨다. 

# 결론

위 예시에서 Sensor를 전혀 변경하지 않고 Sensor가 여러개의 Command를 가지고 있는 것 처럼 동작하게 만들었다. 이런 식의 문제는 SW를 설계하는 데 많이 발생한다. Sensor 와 Command의 관계가 일대일 관계에서 일대다 관계로 바꾸어야 하는 상황에서 일대일 관계를 유지하면서 일대다 행위를 할 수 있게 하였다. 

분명, 일대일 관계를 가지는 SW 설계가 일대다 관계를 가지는 SW 설계보다 이해하기 쉽고 유지보수하기 쉽다. 대신 일대다 관계에서 생기는 복잡성을 컴포지트 클래스가 모두 가지고 있게 된다. 이는 설계상의 Trade-off로 볼 수 있을 것이다.

컴포지트 패턴을 사용할 수 없는 일대다 관계도 있을 것이다. 컴포지트 패턴을 적용하기 위해서는 컴포지트 클래스에 들어갈 모든 객체가 동일하게 취급되어야 하기 때문이다. 하지만 컴포지트 패턴을 적용할 수 있는 경우에는 이 패턴을 적용하여 얻을 수 있는 이점이 충분히 있다는 사실을 알고 적용해야 할 것이다.

---

참고. 로버트C마틴. 클린 소프트웨어 애자일 원칙과 패턴 그리고 실천 방법 (이용원, 김정민, 정지호 옮김) 

참고. "컴포지트 패턴", Wikipedia
