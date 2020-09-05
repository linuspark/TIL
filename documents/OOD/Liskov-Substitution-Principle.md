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

```csharp
public void AssertArea(Rectangle r) {
	r.SetWidth(5);
	r.SetHeight(4);
	Assert.AreEqual(r.GetWidth() * r.GetHeight(), 20);
}
```

---

참고. 로버트C마틴. 클린 소프트웨어 애자일 원칙과 패턴 그리고 실천 방법 (이용원, 김정민, 정지호 옮김)
