[http://www.plantuml.com/plantuml/svg/SoWkIImgAStDuShCAqajIajCJbLmpi_DJSnBgUPIq4x9rz3agkLoICrB0Qe10000](http://www.plantuml.com/plantuml/svg/SoWkIImgAStDuShCAqajIajCJbLmpi_DJSnBgUPIq4x9rz3agkLoICrB0Qe10000)

커맨드 패턴은 단순하다. 인터페이스 하나. 메소드도 없어 보이는 이런 단순한 인터페이스가 어떻게 패턴이 될 수 있는지 의문스러울 정도로 단순한 커맨드 패턴은 이 것이 무슨 효용이 있을지 의문스러울 정도 이다.

사실, 커맨드 패턴은 객체 지향 관점에서 보았을 때 조금 이상할 수 있다. 객체란 변수들과 그 변수들을 이용하는 함수의 집합으로 구성되어 있는데 커맨트 패턴의 경우 함수(실행될 기능)를 캡슐화 해서 변수를 해방시켜 버린다. 즉, 함수의 역활을 클래스의 수준으로 격상시키는 것이다. 

# 단순한 커맨드

다음의 예시는 하드웨어의 장치를 제어하는데 사용된 커맨트 패턴이다.

[http://www.plantuml.com/plantuml/png/SoWkIImgAStDuShCAqajIajCJbLmpi_DJSnBgUPIq4x9rz3agkNYIiv9B2vM24hDIQpqpuFAGmLzyqloY-22A2hJqh0fHOXoeHgee5jQe5jZfm2JXXc2GnfgCJvPt9eTKlDIWBu60000](http://www.plantuml.com/plantuml/png/SoWkIImgAStDuShCAqajIajCJbLmpi_DJSnBgUPIq4x9rz3agkNYIiv9B2vM24hDIQpqpuFAGmLzyqloY-22A2hJqh0fHOXoeHgee5jQe5jZfm2JXXc2GnfgCJvPt9eTKlDIWBu60000)

위 구조는 너무나도 단순하다. Relay On Command에서 Do를 실행하면 Relay가 켜진다. Motor Off Command에서 Do를 실행하면 Motor는 꺼진다. 즉 Command 인터페이스를 들고 있는 모듈은 어떤 모듈이 들어왔는지에 상관없이 Do  명령어를 이용하여 다양한 기능을 수행할 수 있는 것이다.