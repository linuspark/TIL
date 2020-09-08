> 첫째, 상위 모듈은 하위 모듈에 의존해서는 안된다. 상위 모듈과 하위 모듈 모두 추상화에 의존해야 한다.
> 둘째, 추상화는 세부 사항에 의존해서는 안된다. 세부사항이 추상화에 의존해야 한다.
> First. High-level modules should not depend on low-level modules. Both should depend on abstractions(e.g. interfaces)
> Second. Abstractions should not depend on details. Details (concrete implementations) should depend on abstractions.

# 의존 관계 역전 원칙(DIP)

전통적으로 소프트웨어는 상위 모듈이 하위 모듈에 의존하는 형태를 띄고 있다. 보통의 경우 상위 수준의 모듈에서 하위 수준의 모듈을 호출하고 함수에서 서브함수를 호출하는 방식으로 동작하기 때문에 의존성의 방향이 상위 수준의 모듈에서 하위 수준의 모듈로 가도록 SW를 작성하는 것이 일반적이다. 그러나 잘 작성된 객체지향 설계는 전통적인 의존성 구조가 역전되어 있는 구조이다.

보통의 경우 어플리케이션의 정책과 의사결정, 동작 모델 등의 내용을 포함하고 있는 것이 상위 모듈이다. 상위 수준의 모듈은 해당 어플리케이션의 본질을 담고 있다. 그리고 하위 수준의 모듈은 그 어플리케이션의 디테일한 구현 등을 담당한다. 이런 상황에서 디테일한 구현사항이 조금 변경되었을 때 상위 수준의 모듈에 영향을 끼치거나 동작 방식이 변경되어야 하는 구조는 객체지향 설계라고 할 수 없다.

보통 SW에서 변경의 요청으로 발생하는 것은 상위 수준에서 정책이나 방법 등의 요청이다. 그리고 SW를 작성하는 사람으로써 서브루틴을 라이브러리로 만들고 재사용 가능하도록 하는 것이 익숙하다. 만약 상위 모듈이 하위 모듈에 의존성을 가지고 있다면 이런 방식으로 사용하는 것은 불가능 할 것이다. 반면 상위 모듈이 하위 모듈과 독립적으로 존재한다면 상위 모듈을 재사용 하는 것은 훨씬 쉬울 것 이다.

# 레이어

> 잘 구조화 된 모든 객체 지향 아키텍처는 레이어를 분명하게 정의한다. 여기서 각 레이어는 잘 정의되고 제어되는 인터페이스를 통해 일관된 서비스의 집합을 갖는다. - 부치

여기서 가장 중요하게 보아야 할 것은 "잘 정의되고 제어되는 인터페이스" 일 것이다. 아키텍처를 레이어로 나누는 것 보다 인터페이스를 이용하는 것이 더 중요하다고 생각된다.

레이어를 아무리 잘 나눈다 하더라도 각 레이어의 구체적인 클래스 들이 다른 하위 레이어와 직접적인 의존관계를 가진다면 레이어를 나누어 설계한 의미가 반감될 것이다. 상위 레이어의 클래스와 하위 레이어의 클래스가 직접적인 의존 관게를 가진다는 말은 다시 말하면 하위 레이어의 클래스가 수정되었을 때 상위 레이어의 클래스 또한 수정이 필요하게 될 수 있다는 것이다.

아래는 각 레이어의 클래스가 직접적으로 의존 관계에 있는 설계와 각 레이어가 역전된 의존 관계를 가진 설계를 나타낸 것 이다.

```uml
@startuml
class PolicyLayer{}
class MechanismLayer{}
class UtilityLayer{}

PolicyLayer ..> MechanismLayer
MechanismLayer ..>UtilityLayer
@enduml
```

```uml
@startuml
class PolicyLayer{}
class MechanismLayer{}
class UtilityLayer{}

interface PolicyServiceInterface
interface MechanismServiceInterface

PolicyLayer -> PolicyServiceInterface
MechanismLayer ..> PolicyServiceInterface
MechanismLayer -> MechanismServiceInterface
UtilityLayer ..> MechanismServiceInterface
@enduml
```
