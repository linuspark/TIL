# Protocol Oriented Programming

프로토콜 지향 프로그래밍은 Swift 2.0 에서 발표한 새로운 개념의 프로그래밍 패러다임이다. 기존의 객체지향 프로그래밍에서 몇가지 제약사항을 해결하기 위해서 발표되었으며 Swift 는 프로토콜 지향 프로그래밍 언어이다. 

프로토콜 지향 프로그래밍은 기존의 객체지향 프로그래밍의 단점(비용, 안정성 등)을 보완하면서도 객체지향 프로그래밍의 장점(상속 등) 들을 사용하기 위해 고안된 패러다임이다. 

## Swift 에서 이야기하는 Protocol 이란

“Don’t start with a class, start with a protocol”

Swift Documentation에서는 protocol을 아래와 같이 정의한다.

> A *protocol* defines a blueprint of methods, properties, and other requirements that suit a particular task or piece of functionality. The protocol can then be *adopted* by a class, structure, or enumeration to provide an actual implementation of those requirements. Any type that satisfies the requirements of a protocol is said to *conform* to that protocol.

> 프로토콜은 특정 작업이나 기능을 수행하기 위한 메소드, 프로퍼티 또는 기타 요구사항에 대한 청사진을 의미한다. 프로토콜은 해당 요구사항을 구현하기 위해 Class, Structure, Enum 등에 적용되어 사용된다. 프로토콜을 요구사항을 준수하는 모든 타입들은 프로토콜을 준수한다고 이야기한다.

즉, Java나 C#의 Interface 와 동일한 개념이라고 할 수 있다. 다만 기존 Interface와 다른 점은 1. 메서드 뿐만 아니라 필드를 정의할 수 있으며, 2. 클래스 뿐만 아니라 구조체나 Enum에서도 적용될 수 있다. 그리고 3. 구조체나 Enum에도 적용될 수 있기 때문에 값 형식의 인스턴스를 처리하기 위한 Mutating keyward를 사용한다.

정확하게 Interface와 동일한 것은 아니지만 개념상 Swift의 protocol은 기존의 interface가 하는 역할을 수행하고 그에 더해 protocol에 대한 동작을 수행한다.

## Protocol Extension

Swift에서는 Protocol Extension을 통해 POP 를 구성한다. extension이란 말 그대로 "확장" 이라는 의미이다. extension이 protocol에 사용되면 Protocol은 "규약" 만 가지게 되는 것이 아니라 "구현"을 갖게 된다. 즉, Protocol에서 "선언" 된 메소드나 프로퍼티들이 Extension을 통해 실제 "구현"내용을 가지게 되는 것이다.

---

참고. [The Swift Programming Language](https://docs.swift.org/swift-book/LanguageGuide/Protocols.html)

참고. [WWDC-2015, Protocol-Oriented Programming in swift](https://developer.apple.com/videos/play/wwdc2015/408/?time=208)
