# Adapter Pattern

클래스의 인터페이스를 사용자가 원하는 다른 인터페이스로 바꾸어 제공하는 어댑터를 이용하는 패턴이다. 호환성이 없는 인터페이스로 인해 함께 동작할 수 없는 경우 어댑터를 이용하여 함께 동작할 수 있게 만들어낸다.

## Adapter Pattern이 필요한 이유

![http://www.plantuml.com/plantuml/svg/SoWkIImgAStDuKhEIImkLWWkpon9pk3Ap2j9BKfBJ4w52YGcvQHMSoaeQ2kKb1Rb-USXc6bfNBLGlJwPwHabN5mG7GgwTaXwkS1o2hgb1RerAE8EgNafGDi1](http://www.plantuml.com/plantuml/svg/SoWkIImgAStDuKhEIImkLWWkpon9pk3Ap2j9BKfBJ4w52YGcvQHMSoaeQ2kKb1Rb-USXc6bfNBLGlJwPwHabN5mG7GgwTaXwkS1o2hgb1RerAE8EgNafGDi1)

위 예시는 [추상 서버 패턴 (Abstract Server Pattern)](https://www.notion.so/Abstract-Server-Pattern-e77b5ebfc8514daa99d435117d098afe) 에서 사용한 예시이다. Light 가 추상화 인터페이스인 Switchable 를 상속받고 Switch는 추상화에 의존하고 있다. 헌데 Light 가 Switchable 인터페이스를 상속받지 못 하는 상황이라면 추상 서버 패턴을 사용할 수가 없다. 예컨데 Light 는 서드파티에서 가져온 클래스라 직접 변경이 불가능 한 경우가 있을 수 있다. 

어댑터는 이런 문제를 해결할 수 있다.

![http://www.plantuml.com/plantuml/svg/SoWkIImgAStDuKhEIImkLWWkpon9pk3Ap2j9BKfBJ4w52YGcvQHMSoaeQ2kKb1Rb-USXc6bfNBLGlJwPwHabZYc91K2zo49SN11357Jja8pZGbQke5jQe5k3HzeEOfI2bOAIZKrAQavgUc99Qh6TdHANGsfU2j3z0000](http://www.plantuml.com/plantuml/svg/SoWkIImgAStDuKhEIImkLWWkpon9pk3Ap2j9BKfBJ4w52YGcvQHMSoaeQ2kKb1Rb-USXc6bfNBLGlJwPwHabZYc91K2zo49SN11357Jja8pZGbQke5jQe5k3HzeEOfI2bOAIZKrAQavgUc99Qh6TdHANGsfU2j3z0000)

Switchable 을 상속받은 LightAdapter를 구현하고 LightAdapter가 실제 수행할 일을 Light 에게 위임하는 것이다. 이렇게 될 경우 Light 와 Switchable이 다른 인터페이스를 가지고 있더라도 사용이 가능하다. 즉 LightAdapter는 말 그대로 Ligth와 Switchable 사이에서 어댑터 역할을 하고 있는 것이다.

단, 보면 알겠지만 어댑터는 싸게 먹히지 않는 패턴이다. 새로운 클래스도 작성해야 하고, 인스턴스 화 한 어댑터 클래스와 위임하고자 하는 클래스를 연결하는 작업도 해야한다. 다시말해 어댑터 패턴은 사용하지 않을 수 있다면 추상서버 패턴으로도 충분할 수 있다.

## Class 형태의 어댑터

위 예시에서는 어댑터가 말 그래도 중개해 주는 역할을 하며, **객체 형태 어댑터(object from adapter)** 로서 동작한다. 위 어댑터와 다른 접근방식인 **클래스 형태 어댑터(class from adapter)** 도 존재한다. 위 예시를 클래스 형태의 어댑터로 다시 구현한다면 아래와 같은 모양이 된다.

![http://www.plantuml.com/plantuml/svg/SoWkIImgAStDuKhEIImkLWWkpon9pk3Ap2j9BKfBJ4w52YGcvQHMSoaeQ2kKb1Rb-USXc6bfNBLGlJwPwHabZYc91K2zo49SN11357Jja8pZGbQke5jQe5k3Mnee1pNB8JKl1UXS0000](http://www.plantuml.com/plantuml/svg/SoWkIImgAStDuKhEIImkLWWkpon9pk3Ap2j9BKfBJ4w52YGcvQHMSoaeQ2kKb1Rb-USXc6bfNBLGlJwPwHabZYc91K2zo49SN11357Jja8pZGbQke5jQe5k3Mnee1pNB8JKl1UXS0000)

어댑터 클래스인 LightAdapter가 Light를 상속받으므로써 객체 형태보다 조금 더 쉽고 효율적으로 사용할 수 있다. 객체 형태 어댑터의 경우 위임하는 클래스를 연결하는 작업 등을 따로 해 주어야 하지만 클래스 형태 어댑터의 경우 상속받아 구현하기만 하면 된다. 다만 여기에도 장점이 있다면 단점도 존재하는데 상속으로 인한 강한 결합이 생기는 것이다. 

---

참고. 로버트C마틴. 클린 소프트웨어 애자일 원칙과 패턴 그리고 실천 방법 (이용원, 김정민, 정지호 옮김) 

참고. "어댑터패턴", Wikipedia