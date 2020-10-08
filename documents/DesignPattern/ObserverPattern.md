# Observer Pattern

옵저버 패턴에서는 한 객체의 상태가 바뀌면 그 객체에 의존하는 다른 객체들한테 연락이 가고 자동적으로 내용이 갱신되는 방식으로 일대다(one-to-many) 의존성을 정의합니다. 

객체(Subject)의 상태의 변화를 관찰하는 관찰자(Observer)들의 목록을 객체에 등록해 놓고 객체의 상태에 변화가 있을 때 마다 객체가 직접 메서드를 통해 관찰자들에게 알려주도록 하는 디자인 패턴이다. 주로 이벤트 핸들링 시스템을 구현하는데 사용되며 구독/발행 모델로도 알려져 있다.

[OberserPattern.png](http://www.plantuml.com/plantuml/svg/POvB2i9038RtEKMe6nzCyGIbu5v1Jp2TfbAPFaWo1T7UNR4FiDs5B___9QcePGsLXx9Mui8wmaicn1tn2n0FeSsj4lHWCr6sJj5vAuAta3t8wIzpfNifIZmLjxk1Lar7VsnpRhGidXEJB-nXy9sQsZ7fd5_WyHp0EA19ecCSxoES2qi3cj2QTx8Ep8fXFwdNVK-5ccJrGqfr7Yh_0G00)

옵저버 패턴은 한번 이해하면 여기저기서 사용되고 있는 것을 볼 수 있는 유명하고 잘 쓰이는 패턴 중 하나이다. 객체들이 명시적으로 관찰 대상을 호출하도록 작성하는 대신, 서브젝트에 옵저버로 객체를 등록하기만 하면 이벤트가 발생 하였을 때 객체들에게 알려준다. 이런 **간접 참조**는 의존관계를 관리하기 쉽게 만들어 준다. 

## 느슨한 결합

Subject와 Observer가 간접참조를 하고 있다는 것은 서로 느슨한 결합으로 연결되어 있다는 의미이다. 느슨한 결합이라는 것은 서로 상호작용을 하기는 하지만 서로에 대해 서로가 잘 모르고 있다는 것을 의미한다. 

- Subject가 Observer에 대해서 알고 있는 것은 Observer가 update라는 interface를 가지고 있다는 것 뿐이다. 구체적인 구현 클래스가 무엇을 하는지 알 필요가 없다.
- Observer는 언제든지 새로 추가될 수 있다. Observer는 Observer Interface만 구현하고 있으면 되기 때문에 언제든 새로운 구체적인 클래스를 만들고 Subject에 등록할 수 있다. Subject는 구체적인 Observer 클래스가 추가되던, 바뀌던, 제거되던 계속해서 상태를 업데이트 하기만 한다.
- Observer 클래스의 변경사항 때문에 Subject가 변경될 필요가 없다. Observer Interface만 바뀌지 않는다면 Subject 에 영향을 끼치는 것은 없다.
- Subject와 Observer 모두 재사용 가능하다.
- Subject와 Observer 모두 서로에게 영향을 끼치지 않는다. 서로의 Interface만 제대로 구현된다면 Subject의 변경사항이 Observer에게 영향을 주지 않고, 그 반대도 마찬가지이다.

## 패턴의 사용 방식

옵저버 패턴에는 두 가지 사용 방식이 있다. 첫 번째는 **데이터를 끌어오는 방식(Pull-model)의 옵저버 패턴**이다. 이 방식은 서브젝트로 부터 Notify를 받으면 Observer 객체에서 Subject 객체에서 데이터를 끌어오는(Pulling) 방식이다. 이 방식은 구현이 단순하며 Subject 와 Observer 클래스를 재사용 가능한 표준 요소로 라이브러리에 포함시킬 수 있다는 것이 장점이다. 

두 번째 사용 방식은 **데이터를 밀어내는 방식(Push-model)의 옵저버 패턴**이다. 데이터를 밀어내는 방식의 옵저버 패턴은 Notify 함수와 Update함수에 인자가 포함되어 있어 Subject에서 Notify 하는 것의 단서를 전달하는 방식이다. 인자가 어떤 것이든 Subject에서 Observer로 데이터가 전달이 되며 Observer는 이 데이터를 가지고 다음 액션을 수행할 수 있다. 

위 두 방식의 옵저버 패턴의 사용방법은 단순히 관찰 대상이 되는 객체(Subject)의 복잡도에 대한 문제로 이해할 수 있다. 관찰 대상의 객체가 복잡하여 Notify이벤트를 받는 것 만으로는 부족하다면  데이터를 밀어내는 방식이 적합할 것이고, 관찰 대상의 객체가 단순하다면 데이터를 끌어오는 방식을 사용하는 것 만으로도 충분할 것이다. 

## Object Oriented Design

- OCP(Open-Closed Principle): 관찰 대상이 되는 객체(Subject) 가 변경이 되어도 관찰하는 객체(Observer)는 변경하지 않아도 되며 새로 추가하는 것도 가능하다. 즉, 관찰 대상이 되는 객체는 변경에 폐쇄적이다.
- LSP(Liskov Substitution Principle): Concrete Observer를 Observer로 변경하거나 Concrete Subject를 Subject로 변경이 가능하다.
- DIP(Dependency Inversion Principle): Concrete Observer는 Observer에 의존하며 Concrete Subject도 Subject에 의존한다. 간혹 Concrete Observer가 Subject에 의존하는 관계가 있지만 Subject는 추상클래스, 혹은 인터페이스 이기 때문에 Subject 자체로 인스턴스가 생기지 않는다. 즉 Subject는 추상메소드가 하나도 없더라도 논리적으로 보면 추상클래스 이기 때문에 상관이 없다.
- ISP(Interface Segregation Principle): Concrete Class들은 각기 전문화 된 인터페이스를 제공한다.

# 구현 및 사용

객체지향 언어에서는 옵저버 패턴에 대한 내장 인터페이스를 제공하는 경우도 더러 있다.

Java의 경우 java.util.Observer 와 java.util.Observable 을 제공하고, C#의 경우 System.IObservable<T> 와 System.IObserver<T>를 제공한다.

---

참고. 로버트C마틴. 클린 소프트웨어 애자일 원칙과 패턴 그리고 실천 방법 (이용원, 김정민, 정지호 옮김) 

참고. "옵서버 패턴", Wikipedia

참고. 에릭프리먼. Head First Design Pattern (서환수 옮김)

참고. "관찰자 디자인 패턴". MSDN
