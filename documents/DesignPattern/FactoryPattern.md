# Factory Pattern

의존 관계 역전 원칙(DIP)에 따르면 구체적인 클래스에 의존하지 않고 추상 클래스에 의존하는 것을 선호해야 한다. 특히 구체적인 클래스가 쉽게 변하는 종류라면 더더욱 구체적인 클래스에 의존하면 안된다. 다음과 같은 코드는 DIP를 위반하며 구체적인 클래스에 의존하고 있다.

```csharp
Cicle c = new Cicle(origin, r);
```

Circle클래스에 의존하고 있는 코드이다. 즉, new를 사용한다는 것은 특정한 구체적인 클래스에 의존관계를 만든다는 것을 의미한다. 예를 들어 위 코드를 사용하는 모듈이 Circle이 아니라 Square를 필요로 한다면 이 모듈은 크게 변경되어야 할 것 이다. 이 문제를 해결하기 위하여 추상 인터페이스(Shape)를 만들면 다음과 같이 표현될 수 있다.

![http://www.plantuml.com/plantuml/svg/SoWkIImgAStDuKhEIImkLWZEpqrrB2Y0yGfB4ujIeHpdpABad5IkpBoIrAAqnEHKXU2Cn89KBYumfM1JevkINvwd2rM69Wep2MgyWfwU7LIXWfM2ZKroKMfYIQgT7R8yH0iEULqxgEqEgNafGDS30000](http://www.plantuml.com/plantuml/svg/SoWkIImgAStDuKhEIImkLWZEpqrrB2Y0yGfB4ujIeHpdpABad5IkpBoIrAAqnEHKXU2Cn89KBYumfM1JevkINvwd2rM69Wep2MgyWfwU7LIXWfM2ZKroKMfYIQgT7R8yH0iEULqxgEqEgNafGDS30000)

Shape를 상속받는 Square 와 Circle 클래스를 SomeApp이 선택해서 만들 수 있다. SomeApp은 Shape라는 인터페이스를 통해서 Square나 Circle을 사용함으로 인해 사용할 때에 의존성은 분리하였지만 인스턴스를 생성할 때에는 직접 생성하기 때문에 의존 관계를 완전히 분리했다고 할 수는 없다. 이 같은 문제를 팩토리 패턴을 이용하여 해결할 수 있다.

![http://www.plantuml.com/plantuml/svg/XOxDgi8m44RtUOfPtiibVO1B2HL1SDqd6D8HW_c9QOA8zTqLaon2AIxF3D_X37F449FHJ6gSPnYTePttbQu90nNOgo0rCMKZXHDAWl6CViK7bD65-uC1_1cyK5Ry_5REbZS_ixPP7OtNof2D69MpZB7F4_g5J-vcUKrehxMof4E-YfAthGUUF5z44x2MDCzjLzU9KWV_qFSo44OIuikafBUJWUoKZ7u1](http://www.plantuml.com/plantuml/svg/XOxDgi8m44RtUOfPtiibVO1B2HL1SDqd6D8HW_c9QOA8zTqLaon2AIxF3D_X37F449FHJ6gSPnYTePttbQu90nNOgo0rCMKZXHDAWl6CViK7bD65-uC1_1cyK5Ry_5REbZS_ixPP7OtNof2D69MpZB7F4_g5J-vcUKrehxMof4E-YfAthGUUF5z44x2MDCzjLzU9KWV_qFSo44OIuikafBUJWUoKZ7u1)

이렇게 하면 SomeApp은 구체적인 클래스(Circle, Square)에 의존하던 것을 모두 추상 클래스(Shape, ShapeFactory)에만 의존하도록 변경 할 수 있다. 구체적인 클래스에 변경이 발생하더라도 SomeApp에는 영향이 거의 가지 않는다. 

# 의존 관계 순환

위 해결책이 정말로 의존 관계를 분리한 것일까? 

새로운 구체적인 클래스인 Rectangle을 만들어야 한다고 생각해 보자. 구체적인 클래스 Rectangle 클래스를 만들고 이 클래스를 생성하기 위하여 ShapeFactory 에 makeRectangle이라는 함수를 만들어야 한다. 새로운 파생형 클래스가 생길 때 마다 ShapeFactory에 새로운 함수가 추가되어야 하기 때문에 이것은 ShapeFactory를 사용하는 모든 사용자의 클래스를 재 컴파일해야 한다. 의존 관계 순환이 생긴 것이다. 

이런 문제는 타입 안정성을 희생하여 문제를 해결할 수 있다. Shape 파생형 마다 함수를 만드는 대신 String 을 입력받아 원하는 클래스를 만들도록 만들어 주는 것이다.

![http://www.plantuml.com/plantuml/svg/XOvDQiCm48NtEiKiMufyW6A4Iw7GjKymo9D4H3-AD2A4E7SF939469FbcwVtwHioO-BYhD0MSuOnEFg9SKcdWebg-3L9MnB6CwKTQeBnW76L_r1pI9Uh0FXoUAIFpCdu_QUuLSphgtyNhN7a6Ta4BuHubD3FSWfdBvSls-jYLLNXULLLPniFiaGvgqPW3MdARLRNgMe7tz3tEX4oAVLcKjNRoK1-AixU0G00](http://www.plantuml.com/plantuml/svg/XOvDQiCm48NtEiKiMufyW6A4Iw7GjKymo9D4H3-AD2A4E7SF939469FbcwVtwHioO-BYhD0MSuOnEFg9SKcdWebg-3L9MnB6CwKTQeBnW76L_r1pI9Uh0FXoUAIFpCdu_QUuLSphgtyNhN7a6Ta4BuHubD3FSWfdBvSls-jYLLNXULLLPniFiaGvgqPW3MdARLRNgMe7tz3tEX4oAVLcKjNRoK1-AixU0G00)

단, 이렇게 할 경우 인자를 잘못 넘겨준다면 컴파일 에러 대신 런타임 에러가 발생할 수 있음을 알고 있어야 한다. 이 문제의 경우 적절한 단위테스트와 TDD를 이용하여 문제를 피해갈 수 있을 것이다. 

# 테스트를 위한 팩토리

단위테스트를 만들 때 다른 모듈과는 분리된 상태에서 해당 모듈의 기능만을 테스트하고자 할 때가 있다. 예를 들어 데이터베이스에서 데이터를 가져와 처리하는 모듈의 경우 실제 데이터베이스 연결 없이 모듈을 테스트하고자 할 수 있을 것이다.

아래 예시는 Database를 이용하는 Payroll이라는 클래스를 보여준다.

![http://www.plantuml.com/plantuml/svg/SoWkIImgAStDuKhEIImkLWX8h2pApu7nN19B4fCIYrEvkA3Y2hfs2467rBmKe4u0](http://www.plantuml.com/plantuml/svg/SoWkIImgAStDuKhEIImkLWX8h2pApu7nN19B4fCIYrEvkA3Y2hfs2467rBmKe4u0)

실제 Database을 이용하지 않고 Payroll클래스의 기능을 테스트하기 위해 추상인터페이스를 사용하고 테스트를 위하여 Database를 모사하는 PayrollTest 클래스를 만든다. PayrollTest라는 클래스를 이용하여 다른 종류의 DB 를 테스트하거나 에러 상황도 테스트 할 수 있다. 이런 방식을 **스푸핑(Spoofing:위장)** 이라고 한다.

![http://www.plantuml.com/plantuml/svg/SoWkIImgAStDuKhEIImkLWX8h2pApydXoimhIIrAIqnELN19B4bCIYnEXIY0Sprp2t8oSrFpIX9BClFpK7M7f1QNS751EGgwTWWpO0m5cnhTbFpoF5qSvc4gH34RYGqq7kveXzIy5A1N0000](http://www.plantuml.com/plantuml/svg/SoWkIImgAStDuKhEIImkLWX8h2pApydXoimhIIrAIqnELN19B4bCIYnEXIY0Sprp2t8oSrFpIX9BClFpK7M7f1QNS751EGgwTWWpO0m5cnhTbFpoF5qSvc4gH34RYGqq7kveXzIy5A1N0000)

Payroll 클래스가 테스트를 위해서 DatabaseImplimentation대신 PayrolTest를 참조하게 하기 위해서는 다양한 방법이 있을 수 있다. Database 참조를 직접 전달하거나, Database를 참조하는 전역 변수를 설정하거나 하는 방법들이 있다. 하지만 Payroll 클래스 내부에서 Database 인스턴스를 만들어 내야 하는 경우 Payroll 클래스에 다른 팩토리를 넘겨주는 방법으로 Database의 테스트 버전인 PayrollTest를 만들어 낼 수도 있을 것이다.

![http://www.plantuml.com/plantuml/svg/VP112eCm44NtEKKka0iK6LoKGdTTz09Zd1PXaaWoKWGFtq8ZjKRTJVB_VDwVEWb66HmhovYIlk4O0xFgl51ye2LzHi464sN3_BowdZj7Nb2wuF-txvHa8-62La8SitVrkyfJEKeR-17CWwucquQNDtiqfN59jfYr6Ne3iree4nJmXzXxInjbigHFkdfoQ92Xv3eo7tDyMyFEVJunbOs4GW2g9jyEZjy0](http://www.plantuml.com/plantuml/svg/VP112eCm44NtEKKka0iK6LoKGdTTz09Zd1PXaaWoKWGFtq8ZjKRTJVB_VDwVEWb66HmhovYIlk4O0xFgl51ye2LzHi464sN3_BowdZj7Nb2wuF-txvHa8-62La8SitVrkyfJEKeR-17CWwucquQNDtiqfN59jfYr6Ne3iree4nJmXzXxInjbigHFkdfoQ92Xv3eo7tDyMyFEVJunbOs4GW2g9jyEZjy0)

UML이 조금 복잡해 보이는데 결국은 PayrollTest 클래스가 Database 인터페이스와 DatabaseFactory 인터페이스를 상속받아 Factory에서 클래스 생성을 요청할 때 자기 자신을 생성해서 넘겨주는 것을 표현한 것이다. 여기서는 Payroll 클래스가 DatabaseFactory(전역변수)를 통해 database 구현체를 생성하는데 이 DatabaseFactory라는 전역변수를 PayrollTest라는 클래스로 대체하기만 하면 된다. 이렇게 하면 Payroll 클래스에서 Database를 사용하는 모든 호출을 스푸핑 할 수 있다.

# 결론

DIP를 적용하는 것은 중요하다. OOD를 구현하기 위해서는 DIP이 아주 큰 역할을 하기 때문이다. 그리고 DIP 를 지키기 위하여 팩토리 패턴을 사용하는 것은 아주 간단하고 생각하기 쉬운 해결책 이다. 하지만 팩토리 패턴을 사용하는 것은 소프트웨어의 복잡성을 크게 늘리는 것이다. 단순하게 생각해서 팩토리 패턴을 사용하기 위해서는 새로운 클래스와 팩토리의 인터페이스 클래스 2개, 그리고 인터페이스의 구현체 클래스 2개 해서 총 4개나 클래스를 만들어야 한다. 

팩토리는 강력한 도구이지만 이는 피하려면 피할 수도 있는 복잡성이다. Default로 팩토리를 사용하는 것이 최선의 방법이 될 가능성은 드물다. 팩토리의 장점(구체적인 구현에 의존하지 않게 하고 어떤 클래스 무리를 다른 클래스 무리로 교체할 수 있도록 하는 것) 과 단점(설계의 복잡성 증가) 을 이해하고 시의적절하게 사용하는 것이 중요하다.

---

참고. 로버트C마틴. 클린 소프트웨어 애자일 원칙과 패턴 그리고 실천 방법 (이용원, 김정민, 정지호 옮김)
