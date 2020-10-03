# Composite Pattern

![https://upload.wikimedia.org/wikipedia/commons/thumb/5/5a/Composite_UML_class_diagram_%28fixed%29.svg/960px-Composite_UML_class_diagram_%28fixed%29.svg.png](https://upload.wikimedia.org/wikipedia/commons/thumb/5/5a/Composite_UML_class_diagram_%28fixed%29.svg/960px-Composite_UML_class_diagram_%28fixed%29.svg.png)

컴포지트 패턴(Composite pattern)이란 객체들의 관계를 트리 구조로 구성하여 부분-전체 계층을 표현하는 패턴으로, 사용자가 단일 객체와 복합 객체 모두 동일하게 다루도록 한다. - wikipedia

컴포지트 패턴은 아주 단순하지만 가지고 있는 의미는 크다. 위 다이어그램에서 Composite 클래스는 여러 Component 클래스를 가지고 있을 수 있고 하나의 Component (파생) 클래스로 동작할 수 있다. 즉, Composite클래스는 그냥 일반 Component 클래스 이며 하는 행위도 Component 클래스와 다를게 없어 보인다. 하지만 사실 Composite 클래스는 여러 Component 인스턴스 집합의 프록시이다. 

---

참고. 로버트C마틴. 클린 소프트웨어 애자일 원칙과 패턴 그리고 실천 방법 (이용원, 김정민, 정지호 옮김) 

참고. "컴포지트 패턴", Wikipedia
