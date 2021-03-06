# Monostate Pattern

모노스테이트 패턴을 이야기 할 때에는 싱글톤 패턴을 이야기하지 않을 수 없다. 모노스테이트 패턴과 싱글톤 패턴 모두 "단일성"을 이루기 위한 방법으로 매커니즘은 다르지만 "단일 객체"를 표현하기 위한 패턴이기 때문이다.

싱글톤 패턴의 경우 **구조적으로 단일성 구조를 강제**하는 반면 모노스테이트 패턴은 **구조적인 강제 대신 단일성이 있는 "행위"를 강제**한다. 모노스테이트 패턴의 예시 코드는 다음과 같다.

```csharp
public class Monostate {
	private static int itsX = 0;
	public Monostate(){
	}
	public void SetX(int x){
		this.itsX = x;
	}
	public int GetX() {
		return this.itsX;
	}
}
```

모노스테이트 패턴의 인스턴스 들은 모든 인스턴스가 하나의 객체인 것 처럼 동작한다. 모노스테이트의 함수는(생성자도) static이 아니지만 클래스의 맴버 변수는 static으로 구현함으로써 모든 인스턴스의 상태를 동일하게 유지한다.

그래서 혹자는 모노스테이트 패턴을 "개념적인 싱글톤" 이라고 부르거나 "싱글톤의 슈가코드" 라고 부르기도 한다.

## 장점

- **투명성:** 모노스테이트의 사용자는 일반 객체처럼 클래스를 사용할 수 있다. 사용자는 이 객체가 모노스테이트임을 알 필요가 없다. (싱글톤의 경우 사용자가 이 객체는 싱글톤이라는 것을 알고 인스턴스를 부르는 것을 통해 구현되는 것에 비해 모노스테이트는 일반 객체를 호출하듯 객체를 생성하고 사용하면 된다)
- **파생 가능성:** 모노스테이트를 상속하는 파생 클래스는 모노스테이트 가 된다. 파생 클래스는 모두 같은 정적변수를 공유하기 때문에 같은 모노스테이트의 일부가 된다.
- **다형성:** 모노스테이트 패턴의 함수들은 정적 함수들이 아니기 때문에 파생 클래스에서 오버라이드 될 수 있다. 따라서 파생 클래스는 같은 정적 변수 집합에 대하여 다르게 동작할 수 있다.
- **잘 정의된 생성과 소멸:** 모노스테이트의 변수는 생성과 소멸 시기가 잘 정의되어 있다.

## 비용

- **변환 불가:** 보통 클래스는 파생을 통해 모노스테이트로 변환될 수 없다.
- **효율성:** 하나의 모노스테이트 객체는 실제 객체이기 때문에 많은 생성과 소멸을 겪을 수 있다. (비용 발생)
- **실재함:** 모노스테이트의 변수는 실제로 모노스테이트가 사용되지 않는다 하더라도 공간을 차지한다.(static 변수는 객체의 생성과 소멸에 관계없이 프로그램이 시작할 때 할당되고 계속 공간을 차지한다.)
- **플랫폼 한정:** 한 모노스테이트가 여러개의 JVM인스턴스나 여러개의 플랫폼에서 동작하게 만들 수 없다

## 싱글톤과의 비교

싱글톤의 경우 객체를 생성하기 위한 방법을 제한하기 위하여 private생성자, 1개의 정적변수, 1개의 정적함수를 이용한다. 반면 모노스테이트의 경우 그저 객체의 모든 변수를 Static으로 만든다.

싱글톤의 경우 파생을 통해 제어하고 싶은 이미 존재하는 클래스가 있을 때, 그리고 접근 권한을 얻기 위해 싱글톤에 접근하는 모든 곳에서 Instance()를 호출하는 것이 상관이 없을 때 최선의 선택이다. 모노스테이트의 경우 클래스의  본질적 단일성이 사용자에게 투과적이 되도록 하고 싶을 때, 또는 단일 객체의 파생 객체가 다형적이 되게 하고 싶을 때 최선의 선택이다.

---

참고. 로버트C마틴. 클린 소프트웨어 애자일 원칙과 패턴 그리고 실천 방법 (이용원, 김정민, 정지호 옮김) 

참고. "싱글턴 패턴", Wikipedia
