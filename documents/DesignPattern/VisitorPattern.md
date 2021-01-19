문제상황: 클래스의 계층 구조에 새로운 메소드를 추가할 필요가 있을 때, 실제로 클래스의 계층 구조 마다 새로운 클래스를 추가하는 것은 설계를 해치거나 다른 문제를 야기시킬 수 있다.

예를 들어 Modem 의 계층구조에는 Modem 이 수행할 수 있는 동작을 정의한 Modem Interface가 있고 파생형의 여러가지 Modem 구현체가 있다. 이 때 Modem 이 동작에 "특정 OS에서 동작하기 위한 행동 (ConfigureForUnix)" 을 추가하고자 한다면 파생형의 모든 객체에 메소드를 추가해야 한다. 이런 행위는 다른 메소드가 추가될 때 마다 계층 구조를 수정해야 하는 문제가 생긴다.

![http://www.plantuml.com/plantuml/svg/SoWkIImgAStDuVBCAqajIajCJbNmpKz9pLMevj9MSCbCp05ImQbvAK3A8p4llRG0o0XAJIxZgkNYIiv9B2u62bUc5aFPKVdvkL2cQr5UPYeN5rXMGRUqGBV63c8o5qWHgWXOBQgG0z1EeBC0](http://www.plantuml.com/plantuml/svg/SoWkIImgAStDuVBCAqajIajCJbNmpKz9pLMevj9MSCbCp05ImQbvAK3A8p4llRG0o0XAJIxZgkNYIiv9B2u62bUc5aFPKVdvkL2cQr5UPYeN5rXMGRUqGBV63c8o5qWHgWXOBQgG0z1EeBC0)

# Visitor Pattern

알고리즘을 객체 구조에서 분리시키기 위한 패턴. 즉, 기존의 계층구조를 수정하지 않고 새로운 메소드를 계층구조에 추가할 수 있도록 하여 개발-폐쇄 원칙을 지킬 수 있게 한다.

이러한 방식의 패턴을 "비지터 집합"에 속한 디자인 패턴 이라고 하며 다음과 같은 패턴들이 있다.

- 비지터(Visitor)
- 비순환 비지터(Acyclic Visitor)
- 데코레이터(Decorator)
- 확장 객체(Extension Object)

이 중 비지터 패턴의 경우 이중 디스패치(double dispatch)를 사용하여 문제를 해결한다.

## Dispatch

디스패치(Dispatch)란 (메시지 등을) 보내다 라는 뜻을 가진다. 객체지향 프로그래밍 에서 디스패치란 (메시지를 전달하여) 원하는 함수를 호출하는 것을 의미한다.

디스패치는 정적 디스패치(static dispatch)와 동적 디스패치(dynamic dispatch)로 나눌 수 있는데 정적 디스패치(static dispatch)는 컴파일 타임에 어떤 메소드를 선택하여 호출할 지 미리 정해져 있는 것을 의미하고 동적 디스패치(dynamic dispatch)의 경우 런타임에 할당된 객체를 파악하여 메소드를 실행하는 것을 의미한다.

### 정적 디스패치(Static Dispatch)

```csharp
public class Service(){
		public void Run() {}
}

class TestClass
{
    static void Main(string[] args)
    {
				Service service = new Service();
				service.Run() // Service 클래스의 Run을 호출
    }
}
```

### 동적 디스패치(Dynamic Dispatch)

```csharp
interface class Service(){
		public void Run()
}

class ServiceImplA: Service{
		public override Run() { // Do Something 
		}
}

class ServiceImplB: Service{
		public override Run() { // Do Something 
		}
}

class Client(){
		public void UseService(Service service){
				service.Run();
		}
}

class TestClass
{
    static void Main(string[] args)
    {
				var serviceList = new List<Service>();
				serviceList.Add(new ServiceImplA());
				serviceList.Add(new ServiceImplA());

				Client client = new Client();
				
				foreach (var service in serviceList){
						client.UseService(service);
				}
    }
}
```

### 이중 디스패치(Double Dispatch)

동적 디스패치를 두 번 하는 것이다. 즉, 런타임에 전달된 객체의 함수를 실행하는데 (Single Dynamic Dispatch) 실행할 함수에 자기 자신을 인자로 주어 다시 한번 Dynamic Dispatch를 하는 것이다.

```csharp
interface class Service(){
		public void Run(Client client)
}

class ServiceImplA: Service{
		public override Run(Client client) { // Do Something using Client class
		}
}

class ServiceImplB: Service{
		public override Run(Client client) { // Do Something using Client class 
		}
}

class Client(){
		public void UseService(Service service){
				service.Run(this);
		}
}

class TestClass
{
    static void Main(string[] args)
    {
				var serviceList = new List<Service>();
				serviceList.Add(new ServiceImplA());
				serviceList.Add(new ServiceImplA());

				Client client = new Client();
				
				foreach (var service in serviceList){
						client.UseService(service);
				}
    }
}
```

위 예시 코드에서 디스패치가 2번 일어나게 되는데 Client의 UseService 메소드에서 실행할 Service 객체의 Run메소드를 찾기 위해 한 번 일어나고, Service 의 Run 메소드에서 Client의 함수를 사용하기 위해 한번 더 일어난다.

# Visitor Pattern Group

![http://www.plantuml.com/plantuml/svg/ROxDIWH138JlUOe-xY8xZo0BAgm7BueUl8MUp1Zedw5_5cNrtUs4HfrTJwbKYY-rpmLJgTx1VIYK9hHa7k98tfpWojmokZQUA8nj733CTMdYaUon3RIMbhBH-0jdBZ5juGlEIVqalAF8pG4_A6z_rjSO_UzsbmAJOAp3d8rckvPWbve2cDZHlpLEqaCTCmo9vxSo3DUhEg1aiwlBxhDVG1wi7Vspjlv2Z50LT6aBxDBjnPy3l-lj9eQ9vvfG0lhdhEQUmbYz-mO0](http://www.plantuml.com/plantuml/svg/ROxDIWH138JlUOe-xY8xZo0BAgm7BueUl8MUp1Zedw5_5cNrtUs4HfrTJwbKYY-rpmLJgTx1VIYK9hHa7k98tfpWojmokZQUA8nj733CTMdYaUon3RIMbhBH-0jdBZ5juGlEIVqalAF8pG4_A6z_rjSO_UzsbmAJOAp3d8rckvPWbve2cDZHlpLEqaCTCmo9vxSo3DUhEg1aiwlBxhDVG1wi7Vspjlv2Z50LT6aBxDBjnPy3l-lj9eQ9vvfG0lhdhEQUmbYz-mO0)

위 "문제상황" 의 모뎀에 새로운 함수를 추가하고자 할 때 비지터 패턴을 사용하면 위와 같은 방식으로 사용할 수 있다. 

새로 추가된 함수는 accept(ModemVisitor) 라는 함수이다. 이 함수는 ModemVisitor 인스턴스를 인자로 받아 각 클래스에 맞는 동작을 수행하는 역할을 한다.

```csharp
public class Hayes: Modem {
		...
		public void accept(ModemVisitor v) {
				v.visit(this);
		}
}

public class Zoom: Modem {
		...
		public void accept(ModemVisitor v) {
				v.visit(this);
		}
}

public class Ernie: Modem {
		...
		public void accept(ModemVisitor v) {
				v.visit(this);
		}
}

public class UnixModemConfigurator: ModemVisitor {
		public void visit(Hayes modem){
				modem.configuration_something
		}
		public void visit(Zoom modem){
				modem.configuration_something
		}
		public void visit(Ernie modem){
				modem.configuration_something
		}
}
```

방문할 모든 파생형 클래스(Hayes, Zoom, Ernie)마다 비지터 계층에 존재한다. Modem 의 파생형 계층 구조가 ModemVisitor의 메소드로 들어간 모양새 이다. 이렇게 구조를 만들게 되면 ModemVisitor에 새로운 파생형을 만드는 방식으로 새로운 함수를 추가할 수 있다. 즉, ModemVisitor를 상속받는 새로운 클래스를 만들어 다르게 동작하도록 할 수 있는 것이다. 이렇게 하면 새 함수를 추가할 때 마다 Modem 계층구조를 수정할 필요가 없다.

이것이 이중 디스패치라고 불리는 이유는 다형성을 이용해서 어떤 함수를 호출하게 될 지 결정하는 작업(디스패치)을 두 번 수행하기 때문이다. 1) accept()함수가 호출될 때 호출되는 ModemVisitor 인스턴스에 따라 다른 accept() 함수가 호출된다. 2) ModemVisitor 의 visit함수가 호출 될 때 인자로 받는 클래스의 타입에 따라 다른 함수가 호출된다. 

아래는 일반적인 비지터 패턴의 UML 이다.

![https://upload.wikimedia.org/wikipedia/commons/0/00/W3sDesign_Visitor_Design_Pattern_UML.jpg](https://upload.wikimedia.org/wikipedia/commons/0/00/W3sDesign_Visitor_Design_Pattern_UML.jpg)

비지터 패턴의 일반적인 UML

---

참고. 로버트C마틴. 클린 소프트웨어 애자일 원칙과 패턴 그리고 실천 방법 (이용원, 김정민, 정지호 옮김) 

참고. Wikipedia, [비지터 패턴](https://ko.wikipedia.org/wiki/비지터_패턴)