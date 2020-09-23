# Facade Pattern

퍼사드(Facade:외관)는 "건물의 정면" 을 의미한다. 퍼사드 패턴은 퍼사드가 의미하는 것 처럼 커다란 소프트웨어 혹은 복잡하고 일반적인 인터페이스를 가진 모듈에 대해서 간단하고 구체적인 인터페이스를 제공하고자 할 때 사용한다. 

퍼사트 패턴의 장점으로는 다음과 같은 것 들이 있다. 

- 소프트웨어 라이브러리를 사용하기/이해하기 쉽게 해준다.
- 퍼사드 패턴으로 제공되는 코드를 읽기 쉽게 해준다.
- 퍼사드 패턴의 바깥쪽 코드들이 퍼사드 패턴 안쪽 라이브러리 코드들에 의존성을 줄여준다.
- 보기 좋지 않게 작성된 API 들을 보기 좋게 작성된 API 로 감싸준다.

ps. 래퍼(wrapper)가 특정 인터페이스를 준수해야 하며 폴리모픽 기능을 지원해야 하는 경우에는 어댑터 패턴을 사요한다. 단지, 쉽고 단순한 인터페이스를 이용하고 싶을 때 퍼사드 패턴을 이용한다.

# 예시

[http://www.plantuml.com/plantuml/svg/RT1DJaCX50NWEQjWM6Fg2XfIAphIfFfMS0CdByzImCkbcfZktVvKGgpJxoOSpbaM8PQw3Se5AaNVvnmcHpAbU94r9r-TM1AwY5rzAwrlTP74c7NtcnEFaCvcPLFFxX4Wk3hjbShaDZH2lzEExif7q8l5KmeURCmnwPpwa6A4EtwiqI0as29A4ylJ3ln2aKPmqpUK6cI0D5apCZ7yzGl3w_FZbqC-1UrLjuUUcqFrlzBFOrV_YK-VSMv-kwabeZ_i_GC0](http://www.plantuml.com/plantuml/svg/RT1DJaCX50NWEQjWM6Fg2XfIAphIfFfMS0CdByzImCkbcfZktVvKGgpJxoOSpbaM8PQw3Se5AaNVvnmcHpAbU94r9r-TM1AwY5rzAwrlTP74c7NtcnEFaCvcPLFFxX4Wk3hjbShaDZH2lzEExif7q8l5KmeURCmnwPpwa6A4EtwiqI0as29A4ylJ3ln2aKPmqpUK6cI0D5apCZ7yzGl3w_FZbqC-1UrLjuUUcqFrlzBFOrV_YK-VSMv-kwabeZ_i_GC0)

퍼사드 패턴을 잘 보여주는 간략한 예제 UML 이다.

Application은 JAVA SQL, 즉 DB를 관리하기 위해 java.sql 패키지의 내용을 알 필요가 없다. DB 클래스의 store, getProductData, deleteProductData 함수들만 알고 있으면 된다. DB 클래스는 java.sql 이 가지고 있는 복잡성과 일반성 들을 모두 감추는 역할을 하면서 원하는 기능만을 간편한 인터페이스로 제공한다.

퍼사드 패턴의 사용은 개발자가 "모든 데이터베이스 호출은 DB 클래스를 통해서 해야 한다" 라는 규정을 채택했다는 사실을 내포한다. Application 의 코드가 java.sql의 부분을 직접 사용한다면 이는 규정을 위반한 것이다. 이처럼 퍼사드 패턴을 사용한다는 것은 위에서부터 정책을 적용한다는 의미가 된다.

ps. 정책을 위에서 부터 적용하지 않고 아래서 부터 정책을 적용하는 방법으로는 미디에이터 패턴이 있다.

# 결론

퍼사드 패턴은 보통 어떤 규정의 중심이 되며 모든 사람은 그 아래에 있는 객체를 사용하는 것이 아니라 퍼사드를 사용하기로 합의한 것이다. 즉 이런 정책이 크고 가시적이어야 하는 경우에는 퍼사드 패턴을 이용한다.

---

참고. 로버트C마틴. 클린 소프트웨어 애자일 원칙과 패턴 그리고 실천 방법 (이용원, 김정민, 정지호 옮김) 

참고. "퍼사드패턴", Wikipedia