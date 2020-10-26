# Bridge Pattern

브리지 패턴은 구현부에서 추상화 된 계층을 분리하여 각자 독립적으로 변형할 수 있도록 하는 패턴이다.

![https://upload.wikimedia.org/wikipedia/commons/thumb/c/cf/Bridge_UML_class_diagram.svg/800px-Bridge_UML_class_diagram.svg.png](https://upload.wikimedia.org/wikipedia/commons/thumb/c/cf/Bridge_UML_class_diagram.svg/800px-Bridge_UML_class_diagram.svg.png)

즉 계층구조를 구현체와 추상화로 쪼개서 각자 다른 역할을 수행하도록 하는 것이 브리지 패턴의 핵심이다.

위 UML을 보면 Abstraction의 Function은 impl 이라는 Implementor 객체의 Implemantaion() 함수를 호출하는 것으로 동작한다.

위 와 같은 UML로 작성된 코드를 동작시키는 것은 아래와 같다.

```csharp
Abstraction abstraction = new RefinedAbstraction(new ConcreteImplementor());
abstraction.function()
```

RefinedAbstraction을 생성할 때 인자로 ConcreteImplementor 를 준다. 생성자로 ConcreteImplementor를 주던 함수를 통해 주던 중요한 것은 Function 함수에 대한 동작을 ConcreteImplementor 에게 위임한다는 것이다. 즉, Abstraction의 계층 구조는 그대로 두고 동작에 대한 구현을 A class, B class 등으로 연결할 수 있다.

여기서 주의깊게 보아야 할 것은 Abstraction 클래스(혹은 인터페이스) 에서 Impl 과 Function 에 대한 접근 제한자 이다. 

- Impl : protected 등으로 구성된다(low level) 이는 Abstraction 의 파생형 에서만 사용하기 때문이다.
- Function : public 으로 구성된다(high level) Abstaction 의 파생형 클래스를 사용하는 곳 에서 사용 가능한 API 이다.

브리지 패턴을 이용하여 문제를 해결하는 것은 OOD의 관점에서 볼 때 깔끔한 방법일 것이다. 새로운 Impl 가 추가될 때 마다 기존의 구현을 바꾸지 않고 Implementor 파생 클래스를 만들어 준다면 OCP 도 만족하며, Abstraction 부분에 새로운 인터페이스를 추가 할 때 ISP를 적용하여 Interface를 분리할 수도 있다. 

하지만 브리지 패턴은 복잡하다. 그 구조를 알고 있는 사람도 한번은 다시 보게 만드는 복잡함이 있기 때문에 처음부터 브리지 패턴을 적용하고자 생각하는 것은 권장되지 않는다. 

패턴은 언제나 마찬가지로 이점만 있지 않으며 비용또한 존재하기 때문에 현재 상황과 문제에 맞는 패턴을 선택할 줄 알아야 한다.

---

참고. 로버트C마틴. 클린 소프트웨어 애자일 원칙과 패턴 그리고 실천 방법 (이용원, 김정민, 정지호 옮김) 

참고. "브리지 패턴", Wikipedia