# Observer Pattern

객체의 상태의 변화를 관찰하는 관찰자(옵저버)들의 목록을 객체에 등록해 놓고 객체의 상태에 변화가 있을 때 마다 객체가 직접 메서드를 통해 관찰자들에게 알려주도록 하는 디자인 패턴이다. 주로 이벤트 핸들링 시스템을 구현하는데 사용되며 구독/발행 모델로도 알려져 있다.

[http://www.plantuml.com/plantuml/svg/POvB2i9038RtEKMe6nzCyGIbu5v1Jp2TfbAPFaWo1T7UNR4FiDs5B___9QcePGsLXx9Mui8wmaicn1tn2n0FeSsj4lHWCr6sJj5vAuAta3t8wIzpfNifIZmLjxk1Lar7VsnpRhGidXEJB-nXy9sQsZ7fd5_WyHp0EA19ecCSxoES2qi3cj2QTx8Ep8fXFwdNVK-5ccJrGqfr7Yh_0G00](http://www.plantuml.com/plantuml/svg/POvB2i9038RtEKMe6nzCyGIbu5v1Jp2TfbAPFaWo1T7UNR4FiDs5B___9QcePGsLXx9Mui8wmaicn1tn2n0FeSsj4lHWCr6sJj5vAuAta3t8wIzpfNifIZmLjxk1Lar7VsnpRhGidXEJB-nXy9sQsZ7fd5_WyHp0EA19ecCSxoES2qi3cj2QTx8Ep8fXFwdNVK-5ccJrGqfr7Yh_0G00)

옵저버 패턴은 한번 이해하면 여기저기서 사용되고 있는 것을 볼 수 있는 유명하고 잘 쓰이는 패턴 중 하나이다. 객체들이 명시적으로 관찰 대상을 호출하도록 작성하는 대신, 서브젝트에 옵저버로 객체를 등록하기만 하면 이벤트가 발생 하였을 때 객체들에게 알려준다. 이런 간접 참조는 의존관계를 관리하기 쉽게 만들어 준다. 

옵저버 패턴에는 두 가지 사용 방식이 있다. 첫 번째는 데이터를 끌어오는 방식(Pull-model)의 옵저버 패턴이다. 이 방식은 서브젝트로 부터 Notify를 받으면 옵저버 객체에서 서브젝트 객체에서 데이터를 끌어오는(Pulling) 방식이다. 이 방식은 구현이 단순하며 서브젝트와 옵저버 클래스를 재사용 가능한 표준 요소로 라이브러리에 포함시킬 수 있다는 것이 장점이다. 

두 번째 사용 방식은 데이터를 밀어내는 방식의 옵저버 패턴이다. 데이터를 밀어내는 방식의 옵저버 패턴은 Notify 함수와 Update함수에 인자가 포함되어 있어 서브젝트에서 Notify 하는 것의 단서를 전달하는 방식이다. 인자가 어떤 것이든 서브젝트에서 옵저버로 데이터가 전달이 되며 옵저버는 이 데이터를 가지고 다음 액션을 수행할 수 있다. 

위 두 방식의 옵저버 패턴의 사용방법은 단순히 관찰 대상이 되는 객체의 복잡도에 대한 문제로 이해할 수 있다. 관찰 대상의 객체가 복잡하여 Notify이벤트를 받는 것 만으로는 부족하다면  데이터를 밀어내는 방식이 적합할 것이고, 관찰 대상의 객체가 단순하다면 데이터를 끌어오는 방식을 사용하는 것 만으로도 충분할 것이다. 

---

참고. 로버트C마틴. 클린 소프트웨어 애자일 원칙과 패턴 그리고 실천 방법 (이용원, 김정민, 정지호 옮김) 

참고. "옵서버 패턴", Wikipedia
