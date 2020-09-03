>소프트웨어 개체(클래스, 모듈, 함수 등)는 확장에 대해서는 열려있어야 하고, 수정에 대해서는 닫혀있어야 한다.
>Software entities (classes, modules, functions, etc.) should be open for extension, but closed for modification

# 개방 폐쇄 원칙의 속성

1. 확장에 대하여 열려있다.

    열려 있다 라는 말은 자유롭게 드나들 수 있다는 의미를 가진다. 즉, SW의 기능을 확장하는데 자유롭다는 말 이다. SW의 요구사항이 변경되면 해당 요구사항에 맞게 새로운 행위를 추가하여 모듈을 확장할 수 있다. 다시 말하면 모듈이 하고자 하는 행위가 쉽게 변경될 수 있어야 한다는 의미이다.

2. 수정(변경)에 대하여 닫혀있다.

    반대로 수정에 대해서는 닫혀있기 때문에 자유롭지 못 하다. 행위를 추가하거나 요구사항 들이 변경되어 확장될 때  SW가 수정되어서는 안된다. 조금 더 정확하게 말하면 해당 기능을 하던 모듈의 소스코드나 바이너리 코드의 변경이 없어야 한다는 뜻이다.

위 두 가지 속성은 얼핏 보면 서로 상반되고 있다고 느낄 수 있다. 행위를 추가하는 것은 자유롭게 하지만 소스코드가 바뀌면 안된다니? 보통은 기능을 확장할 때 해당 기능을 하는 모듈을 수정하여 기능을 확장하는 방법을 생각한다.

특정 모듈의 소스코드를 바꾸지 않고 해당 모듈의 동작을 바꾸는 것이 가능할까?

# 추상화를 통한 개방 폐쇄 원칙

컴퓨터과학(CS)에서 추상화란 복잡한 자료, 모듈, 시스템 등에서 핵심적인 기능, 개념 등을 간추려 내는 것을 말한다. 객체지향 프로그래밍 언어에서 추상화 라는 것은 추상화 클래스나 인터페이스 등을 이용하여 고정된 기능을 만들고 파생클래스 에서는 기능을 자세하게 정의하여 사용할 수 있도록 하는 것 이다. 

모듈은 추상화된 클래스의 고정된 기능들 만을 이용하기 때문에 수정에 대해서는 닫혀 있다고 할 수 있다. 또한 그 모듈의 행위가 변경이나 확장되었을 때 새로운 파생 클래스를 만듦으로써 확장이 가능하다. 즉 확장에는 열려있는 것이다.

예시) 아래 예시는 Client 에서 Server를 이용하는 예시이다. 

```csharp
public class Client{
	private Server _server;

	public void RequestSomething(){
		this._server.Request("RequestMessage")
	}
}
public class Server{
	public void Request(string msg){}
}
```

Client 는 Server를 직접 사용한다. 위 상황에서 다른 Server로 ServerB 라는 클래스를 사용하기 위해서는 Client가 새로운 서버를 지정하도록 변경해야 할 것이다.

Case 1)

아래는 OCP를 따르기 위해 스트래터지 패턴으로 수정한 코드이다.

```csharp
interface ClientInterface{
	void Request(string msg);
}
public class Client{
	private ClientInterface _clientInterface;

	public void ReqeustSomething(){
		this._clientInterface.Request("ReqeustMessage");
	}
}
public class Server : ClientInterface{
	public void Request(string msg){}
}
```

Client가 새로운 서버인 ServerB를 사용하기 위해서는 ClientInterface를 상속받는 ServerB를 새로 구현한 뒤에 Client랑 연결시켜 주면 된다. 이런 방식으로 처리하면 Client는 변경될 필요가 없고 Server클래스 또한 변경이 필요없다.

Case 2)

아래는 OCP 를 따르기 위해 템플릿 메소드 패턴으로 수정한 코드이다.

```csharp
public class Client{
	private Server _server;

	public void RequestSomething(){
		this._server.Request("RequestMessage")
	}
}
public abstract class Server{
	public void abstract Request(string msg){}
}
public class ServerA: Server{
	public void override Request(string msg){}
}
```

이 경우에도 새로운 서버인 ServerB 를 연결해서 사용하기 위해서는 추상클래스 Server를 상속받은 ServerB를 새로 구현한 뒤에 Client랑 연결시켜 주면 된다. 이런 방식으로도 OCP를 만족시킬 수 있다.

# 자연스러운 구조

SRP도 마찬가지 이지만 OCP 또한 변경 사항이 발생하였을 때 그 구조를 OCP에 맞도록 바꾸는 작업을 하는 것이 가장 중요하다.

이게 무슨 의미냐 하면 SW설계 단계에서 "A라는 부분은 B로 바뀔 수 있기 때문에 Interface로 기능을 분리시키고..." 와 같은, 미리 변경의 축을 예상해서 더 좋은 설계로 만들고자 하는 작업은 위험하다는 의미이다. 자칫 잘못하면 미리 준비한 설계가 사용되지 않은 채로 불필요한 복잡성만을 가지게 될 수도 있다. 때문에 불필요한 추상화를 이용하여 설계에 부하를 주지 않기 위해서는 실제로 그 추상화가 사용될 때 까지 기다렸다가 바꾸는 것이 차라리 낫다. 

**어설픈 추상화를 피하는 것은 추상화를 하는 것 만큼이나 중요한 일이다.**

추상화를 사용해야 할 때 까지 기다렸다가 해당 변경사항이 발생하였을 때 추상화를 하기로 결정 하였다면 아래와 같은 방법을 사용해 보는 것도 좋다. 

- 테스트를 먼저 작성한다. → 테스트를 먼저 작성함으로써 시스템을 테스트 가능하게 만들 수 있다.
- 아주 짧은 주기로 SW를 작성한다
- 구조를 개발하기 보다 기능을 먼저 개발하고 이를 이해당사자에게 자주 보여준다.
- 가장 중요한 요소를 가장 먼저 개발한다.

즉, SW를 빨리, 그리고 자주 릴리즈하고 가능한 빠르고 가능한 많이 고객과 사용자에게 보여줌으로써 변경의 축과 수정사항을 빠르게 접하고 적용하는 방법이다.

# 결론

OCP는 객체지향 설계의 심장이라고 할 수 있을 만큼 중요한 개념이다.

OCP를 이용함으로써 우리는 객체지향이 바라는 목적(유연성, 재사용성, 유지보수성)을 달성하는 SW를 구현할 수 있다. 이는 객체지향언어를 사용하는 것 만으로는 달성할 수 없으며 아주 주의 깊게 OCP를 사용할 것인지 그렇지 않을 것 인지를 판단해야 한다. 좋은 설계를 바란다고 여기저기 추상화를 마구 적용하는 것은 좋은 설계가 아니다. 

다시 한번 강조하지만 **어설픈 추상화를 피하는 것은 추상화를 하는 것 만큼이나 중요하다.**  

---

참고. 로버트C마틴. 클린 소프트웨어 애자일 원칙과 패턴 그리고 실천 방법 (이용원, 김정민, 정지호 옮김)
