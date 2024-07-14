# Proxy Pattern

프록시(Proxy)는 일반적으로 대리인, 대리권 등을 의미하며 컴퓨터 분야에서는 무언가가 연결될 때 인터페이스의 역할을 하는 어떠한 것을 의미한다. 디자인 패턴에서 **프록시 패턴이란 어떤 객체에 대한 접근을 제어하는 용도의 대변인/대리인 의 역할을 하는 객체를 제공하는 패턴**을 의미한다.

즉, 실제 객체를 이용하는 대신 동일한 인터페이스를 가진 대리 객체(Proxy Object)를 이용하여 로직의 흐름을 제어하는 패턴이다.

![https://upload.wikimedia.org/wikipedia/commons/thumb/7/75/Proxy_pattern_diagram.svg/878px-Proxy_pattern_diagram.svg.png](https://upload.wikimedia.org/wikipedia/commons/thumb/7/75/Proxy_pattern_diagram.svg/878px-Proxy_pattern_diagram.svg.png)

위 UML은 프록시 패턴이 동작하는 방식을 보여준다. 패턴이 적용되는 객체는 세 부분이 있는데 첫 번째 부분은 Client 가 호출할 필요가 있는 모든 메서드가 정의된 인터페이스 부분이고 두 번째는 실제 구현의 동작이 포함된 RealSubject 부분이다. 이 부분에서는 로직적인 부분을 담당하여 처리한다. 그리고 마지막으로 세 번째 부분은 RealSubject를 가지고 있는 Proxy 부분이다. Proxy 부분에서는 RealSubject 에게 동작을 위임(delegate)하여 동작을 수행할 수 있다.

# Example

```csharp
public interface Product {
	public int GetPrice();
	public string GetName();
	public string GetSku();
}
```

Product는 상품 정보를 가지고 있으며 이 상품 정보에 대한 내용은 DB에 저장되어 있다고 가정하자. Client는 DB에 대한 지식 없이 Product에 대한 처리를 원하기 때문에 필요한 정보를 얻을 수 있는 Product라는 Interface를 만들었다.

이 문제를 Proxy를 통해 해결하면 다음과 같은 UML을 그릴 수 있다.

![http://www.plantuml.com/plantuml/svg/TOz12i8m44NtSugvG780AQ7KRjnvXP1CQs2QIZ951GzlnK6iukxpt-V1Rwlu8il44DZNYdjEb0LI5Yg33uJ7CiSbYEA-qw1rtwtXUjkMX-dC02yJMblIU19htLi5e0cRkudp9PiltH-kvkqMZVkakCEcYSGqUY7du6VDD8XnpoCjvRWUVm00](http://www.plantuml.com/plantuml/svg/TOz12i8m44NtSugvG780AQ7KRjnvXP1CQs2QIZ951GzlnK6iukxpt-V1Rwlu8il44DZNYdjEb0LI5Yg33uJ7CiSbYEA-qw1rtwtXUjkMX-dC02yJMblIU19htLi5e0cRkudp9PiltH-kvkqMZVkakCEcYSGqUY7du6VDD8XnpoCjvRWUVm00)

Client는 Product 인터페이스를 이용하며 실제로는 ProductDBProxy를 사용한다. ProductDBProxy 는 DB 에 대한 처리를 담당하고 ProductImpl 에게 로직적인 문제를 위임하여 동작한다. 그렇게 되면 ProductImpl은 DB에 대한 지식 없이 데이터를 처리할 수 있다. 

![http://www.plantuml.com/plantuml/svg/NKyx3i8m3Drz2e-jAYx0WAgIXQrN28c1Y3IfN0ULszE8PcWc-ttiP_UBQ9OqUNWvI_Y8KUvn1MqaCbwzeo00_ugd2uuSRJAYXgrPlzXrPtoIZEmCDIqSrUnNGxOm2JlwqAutopkrO9YqKDbucsOFQYWPXM6InA5GLK1bhexPH-SCZw2dOBUFVm00](http://www.plantuml.com/plantuml/svg/NKyx3i8m3Drz2e-jAYx0WAgIXQrN28c1Y3IfN0ULszE8PcWc-ttiP_UBQ9OqUNWvI_Y8KUvn1MqaCbwzeo00_ugd2uuSRJAYXgrPlzXrPtoIZEmCDIqSrUnNGxOm2JlwqAutopkrO9YqKDbucsOFQYWPXM6InA5GLK1bhexPH-SCZw2dOBUFVm00)

# 서드파티 API

보통의 경우 서드파티 API 등을 사용할 때 프록시의 구현을 생각하게 될 수 있다. 아니 서드파티 API 와 내가 작성하는 애플리케이션 간의 분리를 위해 프록시를 생각해 볼 수 있다.

보통 애플리케이션에서 서드파티 API를 사용하는 경우 다음과 같이 사용한다.

![http://www.plantuml.com/plantuml/svg/SoWkIImgAStDuIhEpimhI2nAp5L8piyjoCzBpIi9BgdCILKeIaqkISnBpqdbuefsB2Z8oKnEBCdCpujLqBLJY7OCy8pbSaZDIm4Q0G00](http://www.plantuml.com/plantuml/svg/SoWkIImgAStDuIhEpimhI2nAp5L8piyjoCzBpIi9BgdCILKeIaqkISnBpqdbuefsB2Z8oKnEBCdCpujLqBLJY7OCy8pbSaZDIm4Q0G00)

이렇게 사용할 경우 애플리케이션은 서드파티 API에 종속되게 된다. 간단하게 사용하는 API 면 상관이 없지만 프로그램이 복잡해 질 수록 API와 나의 애플리케이션은 결합이 크게 증가한다. 이런 문제를 해결하기 위해 중간에 레이어 를 만들고 애플리케이션은 레이어를, 레이어는 API 를 이용하게 만들어 API와의 종속성을 분리할 수 있다.

![http://www.plantuml.com/plantuml/svg/SoWkIImgAStDuIhEpimhI2nAp5L8piyjoCzBpIi9BgdCILKeIaqkISnBpqdbuefsB2Z8oKnEBCdCpujLqBLJYFP9h4mjYkM2q10Xnm3FM2w7rBmKeAa0](http://www.plantuml.com/plantuml/svg/SoWkIImgAStDuIhEpimhI2nAp5L8piyjoCzBpIi9BgdCILKeIaqkISnBpqdbuefsB2Z8oKnEBCdCpujLqBLJYFP9h4mjYkM2q10Xnm3FM2w7rBmKeAa0)

레이어를 이용하여 직접적인 종속성은 분리하였지만 애플리케이션에서 API 로 전이 종속성이 존재한다. 이런 간접적인 종속성도 문제가 될 수 있다. 이 문제를 해결하기 위해서는 레이어와 애플리케이션과의 종속성을 뒤집을 필요가 있고 그렇게 되면 다음과 같이 구현이 된다.

![http://www.plantuml.com/plantuml/svg/BSKn2iCm3030NQ_G1_A3KfAnqA7GqNWGhYYcaYmKUV3lk-IMsy-aoAa2vw-RKv1Y6-h3sFATInY3Mv9zXG7AuIwzKVPX5MyRbYSjZWhNkDsn7Az7XPtjCrN-](http://www.plantuml.com/plantuml/svg/BSKn2iCm3030NQ_G1_A3KfAnqA7GqNWGhYYcaYmKUV3lk-IMsy-aoAa2vw-RKv1Y6-h3sFATInY3Mv9zXG7AuIwzKVPX5MyRbYSjZWhNkDsn7Az7XPtjCrN-)

이렇게 되면 애플리케이션은 API를 알지 못 하고, API는 애플리케이션을 알지 못 한다. 레이어가 중간에서 둘 모두를 알고있어야 하는 것이다. 이렇게 종속성을 재배치 하므로써 프록시 패턴이 이루고자 하는 목적을 이룰 수 있게 된다. 애플리케이션과 API의 관계정보는 레이어에 집중하게 된다.

이 말은 레이어에 악몽이 집중된다는 것 이다. API 가 변경되거나 애플리케이션이 변경될 때 마다 레이어가 영향을 받게 된다. 하지만 악몽은 어디에 위치하는지 알고있는 편이 애플리케이션 전체에 악몽이 퍼지게 되는 것 보다 낫다.

---

참고. 로버트C마틴. 클린 소프트웨어 애자일 원칙과 패턴 그리고 실천 방법 (이용원, 김정민, 정지호 옮김) 

참고. "브리지 패턴", Wikipedia