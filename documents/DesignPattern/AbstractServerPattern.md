# Abstact Server Pattern

추상 서버 패턴이라고 불리는 패턴은 사실 패턴이라고 부르는 것이 민망할 정도로 단순한 패턴이다. 상위 모듈이 구체적인 하위 모듈에 의존하지 않게 모듈 사이에 인터페이스를 두어 추상화에 의존하도록 하는 것이다. 즉 DIP를 지키기 위하여 할 수 있는 가장 간단한 패턴이다.

![http://www.plantuml.com/plantuml/svg/SoWkIImgAStDuKhEIImkLWWkpon9pe1oV3BJCqggkHGKj1LAIelo_FqGpBGqhbekBeXg1LqxY58kXzIy5A1P0000](http://www.plantuml.com/plantuml/svg/SoWkIImgAStDuKhEIImkLWWkpon9pe1oV3BJCqggkHGKj1LAIelo_FqGpBGqhbekBeXg1LqxY58kXzIy5A1P0000)

위 구조는 Swich가 Light 클래스에 의존하고 있는 모습이다. 하지만 Switch라는 클래스는 이름에서도 볼 수 있듯이 Light 만을 위하여 존재하지는 않을 것이다. Light 를 켜고 끌 수도 있지만 추 후에 추가될 Fan을 켜고 끌 수도 있을 것이다. 따라서 Light 라는 클래스만 있을 때는 상관이 없지만 Fan 이라는 클래스가 추가된다면 다음과 같이 바뀔 수 있다.

![http://www.plantuml.com/plantuml/svg/SoWkIImgAStDuKhEIImkLWWkpon9pk3Ap2j9BKfBJ4w52YGcvQGgL7CfA6Whb9GMvVdx8PXfQLorKCq-cUaP9L2sMs8U5nT4iuAk7P8nN61L2hgb1RerAE907LX47LBpKe3E0m00](http://www.plantuml.com/plantuml/svg/SoWkIImgAStDuKhEIImkLWWkpon9pk3Ap2j9BKfBJ4w52YGcvQGgL7CfA6Whb9GMvVdx8PXfQLorKCq-cUaP9L2sMs8U5nT4iuAk7P8nN61L2hgb1RerAE907LX47LBpKe3E0m00)

이렇게 중간에 추상화(Abstract) 된 인터페이스(Server)를 둠으로써 DIP를 만족시키는 패턴을 추상 서버 패턴이라고 한다.

# 인터페이스의 소유

여기서 한 가지만 더 짚고 넘어가면, 인터페이스의 이름이 Switchable 이라는 점이다. 추상 서버 패턴에서 인터페이스는 보통 구체적인 클래스(여기서는 Light나 Fan 클래스)와 함께 묶이기 보다 클라이언트(Switch클래스)와 함께 묶이게 된다. 다시 말해, 클라이언트가 인터페이스를 소유 할 가능성이 높다. 

---

참고. 로버트C마틴. 클린 소프트웨어 애자일 원칙과 패턴 그리고 실천 방법 (이용원, 김정민, 정지호 옮김)