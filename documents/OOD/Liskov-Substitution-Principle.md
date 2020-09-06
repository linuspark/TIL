> 서브타입(Subtype)은 그것의 기반 타입(Base type)으로 치환 가능해야 한다.

# 리스코프 치환 원칙(LSP)

자료형 S가 자료형 T의 하위형 일 때, 프로그램에서 자료형 T의 객체는 프로그램의 속성을 변경하지 않고 자료형 S로 교체할 수 있다. 

즉 서브타입, 상속받은 클래스의 객체는 부모클래스의 위치나 자리에 가서 동작하더라도 "의도한 대로" 동작이 가능해야 한다는 의미이다.

사실 상속을 받아서 클래스를 구현하였다면 당연히 자식 클래스는 부모클래스의 모든 함수를 (그대로 사용하던, 오버라이드 해서 사용하던)사용할 수 있기 때문에 당연한 말을 하는 것 처럼 보인다.  부모클래스의 함수 A는 자식클래스도 사용할 수 있는 것이 당연하기 때문이다.

하지만 리스코프 치환원칙에서 이야기 하고자 하는 것은 그저 돌아가는 "구현" 에 대한 것이 아니다. 상속 계층 구조의 바람직한 방법은 무었인가? OCP를 따르지 않도록 계층구조를 작성해 버리는 함정에 대한 것은 어떤 것이 있는가에 대한 이야기 이다. LSP 의 위반은 OCP의 위반으로 이어지기 때문이다.

# 미묘한 LSP 위반

직사각형과 정사각형의 예시.

1. 직사각형 클래스를 사용하는 어플리케이션을 개발하였다. 
2. 시간이 지나 정사각형 클래스를 추가해야 한다.
3. 일반적인 개념상 모든 정사각형은 직사각형 이기 때문에 (Is-A관계) 직사각형 클래스를 상속받아 정사각형을 구현하였다.

이제 코드로 보자

```csharp
public class Rectangle{
	private int _width;
	private int _height;
	public virtual void SetWidth(int w){ this._width = w; }
	public virtual void SetHeight(int h){ this._height = h; }
	public virtual int GetWidth(){ return this._width; }
	public virtual int GetHeight(){ return this._height; }
}

public class Square: Rectangle{
	public override void SetWidth(int w){ base.SetWidth(w); base.SetHeight(w); }
	public override void SetHeight(int h){ base.SetWidth(w); base.SetHeight(w); }
	public override int GetWidth(){ return base.GetWidth(); }
	public override int GetHeight(){ return base.GetHeight(); }
}
```

Square 의 가로를 변경해도 세로를 변경해도 정사각형이기 때문에 가로/세로가 동시에 바뀌는 것이 맞다. 또한 가로/세로 어떤 값을 가져오더라도 같은 값을 가져오는 것이 맞다. 수학적으로 완벽하다.

Square에 어떤 동작을 시켜도 의도한 정사각형의 역할을 잘 수행해 낸다.

Rectangle에 어떤 동작을 시켜도 의도한 직사각형의 역할을 잘 수행해 낸다.

Rectangle의 참조에 Square 객체를 넘겨줘도 정상적으로 받아지고 정사각형의 역할을 잘 수행해 낸다.

그럼 이제 사용자 입장에서 아래와 같이 함수를 작성해서 사용 한다고 생각해 보자.

직사각형 클래스를 입력으로 받아 가로, 세로를 설정하고 그 면젹을 구해서 확인하는 코드이다. 

```csharp
public void AssertArea(Rectangle r) {
	r.SetWidth(5);
	r.SetHeight(4);
	Assert.AreEqual(r.GetWidth() * r.GetHeight(), 20);
}
```

위 예시의 경우 직사각형 클래스를 입력으로 넣으면 정상적으로 동작하지만 정사각형을 입력으로 넣으면 실패한다. 

사용자의 입장에서 보면, 높이를 변경하는 동작이 가로 또한 변경할 것 이라고 생각하지 않는 것이 합리적이다. 하지만, Rectangle 로 넘겨지는 모든 객체가 이 가정을 만족하지는 않는다.(Square의 경우) Rectangle 에서는 잘 동작하지만 Ractangle을 상속받은 Square에서는 잘 동작하지 않는 다는 것은 Square가 Rectangle에 대해서 치환 가능하지 않다고 말할 수 있으며, 이는 LSP를 위반한다.

LSP는 모델만 별개로 보고, 그 모델의 유효성을 충분히 검증할 수 없다 라는 주요한 결론을 내린다. 모델에 대한 유효성은 오직 고객의 관점에서만 표현될 수 있는 것이다. 위 예시에서 Rectangle에 대한 클래스, Square에 대한 클래스를 별개로 각기 검사한다면 이 클래스 구조는 모순이 없고 유효하다고 이야기 할 수 있을 것 이다.  

하지만 기반 클래스에 대해서 합리적이라고 생각했던 가정을 가지고 함수를 작성하는 프로그래머 입장에서는 이 모델은 유효하지 못 하다. 특정 설계가 적절한지 적절하지 않은 설계인지 확인 하는 겻은 개별 클래스를 확인해서는 부족하다. **그 설계를 사용하는 사용자 입장에서 합리적이라고 생각하는 가정의 관점에서 봐야 한다.** (이런 점에서 기반 클래스를 위한 단위테스트를 적성해 놓았다면 빠르게 오류를 찾을 수 있다.

# 클래스의 행위

"Square" IS A "Rectangle" 이 성립되지 않는 것인가 라고 생각할 수 있을 것이다. 일반적인 수학의 관점에서 보았을 때에는 Square is a Rectangle의 관계가 성립된다. 하지만 우리 프로그래머 의 관점에서는 조금 다르다. 프로그래머 들은 IS-A 관계를 생각 할 때, 각 객체의 행위를 보아야 한다. 즉 "Square의 행위" IS A "Rectangle 의 행위"를 생각해 보아야 하는 것이다. 

Square의 SetWidth와  Rectangle의 SetWidth는 일치하지 않는다. 따라서 Square is a Rectangle은 성립하지 않는다.

LSP는 ODD에서 IS-A 관계는 합리적으로 가정할 수 있고 클라이언트가 의존하는 행위와 관련이 있다는 점을 분명히 말한다. 

# 결론

OCP는 ODD 에서 매우 중요한 핵심적인 원칙이라고 할 수 있다. 그리고 LSP는 OCP를 만족시키기 위한 중요한 요인 중에 하나이다. 기반 타입으로 작성된 모듈을 수정 없이 확장 가능하도록 서브 타입을 만들 수 있도록 하며 서브타입은 기반타입으로 치환이 가능해야 한다. 이 치환 가능성이란 개발자가 깊게 생각하지 않아도 확인할 수 있어야 하며 그러기 위해서는 기반타입에 대한 계약상황(인터페이스 등)을 코드에서 충분히 테스트하여야 한다. 

---

참고. 로버트C마틴. 클린 소프트웨어 애자일 원칙과 패턴 그리고 실천 방법 (이용원, 김정민, 정지호 옮김)
