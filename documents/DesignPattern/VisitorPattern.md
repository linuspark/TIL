문제상황: 클래스의 계층 구조에 새로운 메소드를 추가할 필요가 있을 때, 실제로 클래스의 계층 구조 마다 새로운 클래스를 추가하는 것은 설계를 해치거나 다른 문제를 야기시킬 수 있다.

예를 들어 Modem 의 계층구조에는 Modem 이 수행할 수 있는 동작을 정의한 Modem Interface가 있고 파생형의 여러가지 Modem 구현체가 있다. 이 때 Modem 이 동작에 "특정 OS에서 동작하기 위한 행동 (ConfigureForUnix)" 을 추가하고자 한다면 파생형의 모든 객체에 메소드를 추가해야 한다. 이런 행위는 다른 메소드가 추가될 때 마다 계층 구조를 수정해야 하는 문제가 생긴다.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a7e36b4f-9e6b-4369-95d6-89c70cb6dc83/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a7e36b4f-9e6b-4369-95d6-89c70cb6dc83/Untitled.png)

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
