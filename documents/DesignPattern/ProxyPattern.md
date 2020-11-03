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

---

참고. 로버트C마틴. 클린 소프트웨어 애자일 원칙과 패턴 그리고 실천 방법 (이용원, 김정민, 정지호 옮김) 

참고. "브리지 패턴", Wikipedia
