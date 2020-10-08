![http://www.plantuml.com/plantuml/svg/SoWkIImgAStDuShCAqajIajCJbLmpi_DJSnBgUPIq4x9rz3agkLoICrB0Qe10000](http://www.plantuml.com/plantuml/svg/SoWkIImgAStDuShCAqajIajCJbLmpi_DJSnBgUPIq4x9rz3agkLoICrB0Qe10000)

커맨드 패턴은 단순하다. 인터페이스 하나. 메소드도 없어 보이는 이런 단순한 인터페이스가 어떻게 패턴이 될 수 있는지 의문스러울 정도로 단순한 커맨드 패턴은 이 것이 무슨 효용이 있을지 의문스러울 정도 이다.

사실, 커맨드 패턴은 객체 지향 관점에서 보았을 때 조금 이상할 수 있다. 객체란 변수들과 그 변수들을 이용하는 함수의 집합으로 구성되어 있는데 커맨트 패턴의 경우 함수(실행될 기능)를 캡슐화 해서 변수를 해방시켜 버린다. 즉, 함수의 역활을 클래스의 수준으로 격상시키는 것이다. 

# 단순한 커맨드

다음의 예시는 하드웨어의 장치를 제어하는데 사용된 커맨트 패턴이다.

![http://www.plantuml.com/plantuml/png/SoWkIImgAStDuShCAqajIajCJbLmpi_DJSnBgUPIq4x9rz3agkNYIiv9B2vM24hDIQpqpuFAGmLzyqloY-22A2hJqh0fHOXoeHgee5jQe5jZfm2JXXc2GnfgCJvPt9eTKlDIWBu60000](http://www.plantuml.com/plantuml/png/SoWkIImgAStDuShCAqajIajCJbLmpi_DJSnBgUPIq4x9rz3agkNYIiv9B2vM24hDIQpqpuFAGmLzyqloY-22A2hJqh0fHOXoeHgee5jQe5jZfm2JXXc2GnfgCJvPt9eTKlDIWBu60000)

위 구조는 너무나도 단순하다. Relay On Command에서 Do를 실행하면 Relay가 켜진다. Motor Off Command에서 Do를 실행하면 Motor는 꺼진다. 즉 Command 인터페이스를 들고 있는 모듈은 어떤 모듈이 들어왔는지에 상관없이 Do  명령어를 이용하여 다양한 기능을 수행할 수 있는 것이다.

# 되돌리기

![http://www.plantuml.com/plantuml/svg/SoWkIImgAStDuShCAqajIajCJbLmpi_DJSnBgUPIKD1EoTVG1D6bUM1MBPT3QbuAK3a0](http://www.plantuml.com/plantuml/svg/SoWkIImgAStDuShCAqajIajCJbLmpi_DJSnBgUPIKD1EoTVG1D6bUM1MBPT3QbuAK3a0)

Command 패턴과 스택을 이용해서 Undo 기능을 쉽게 구현할 수 있다.

Command 의 파생 클래스에서 do 의 액션을 구체적으로 기억한 뒤에 undo는 do의 액션을 취소할 수 있도록 구현한다면 되돌리기 기능은 스택에 저장된 클래스 들을 순차적으로 꺼내서 undo 만 해 주면 된다.

되돌리기의 예시로는 그림판 어플리케이션을 예시로 들 수 있다. 그림판 에서는 여러가지 도형과 직선, 곡선 등 다양한 기능을 포함하고 있다. 각각의 기능들이 커맨드 패턴에 따라 구현되어 있다고 생각하면 아래와 같은 클래스 다이어 그램을 상상할 수 있다.

![http://www.plantuml.com/plantuml/svg/SoWkIImgAStDuShCAqajIajCJbLmAKeiJqpAIQtcKb3Gpam1aIb08GrD4AieDJU_B1N8hkNYIiv9B2vMSCuiIiv9XMc22WQb9fSavgLZYFjavg4BXQHMbC25k51DKz0jBT2jiLE0oqFDnQC2Q0DkIP1TE2KTKlDIW2410000](http://www.plantuml.com/plantuml/svg/SoWkIImgAStDuShCAqajIajCJbLmAKeiJqpAIQtcKb3Gpam1aIb08GrD4AieDJU_B1N8hkNYIiv9B2vMSCuiIiv9XMc22WQb9fSavgLZYFjavg4BXQHMbC25k51DKz0jBT2jiLE0oqFDnQC2Q0DkIP1TE2KTKlDIW2410000)

그림판에 원을 그리는 경우 CircleDrawable 인스턴스를 하나 생성하고, draw() 함수를 이용하여 원을 그린다. draw함수는 마우스 이벤트에 따라 원을 그리고 그려진 원 객체의 ID를 자신의 내부 변수 id필드에 저장한 뒤 반환한다. 원 그리기가 완료되면 CircleDrawable 인스턴스를 완료된 명령 스택에 넣는다.

그림판에 그리기 이벤트가 생길 때 마다 위와 같은 방식으로 동작 하다가. "되돌리기" 기능을 사용할 때에는 완료된 명령 스택에서 Drawable 객체를 하나 꺼내 remove 함수를 실행하면 된다. 어느 객체가 꺼내지든간에 꺼내진 객체는 자신이 가지고 있는 id를 기준으로 그려진 객체를 찾고 그림판에서 해당 객체를 지우면 된다.

위와 같은 방법으로 취소(되돌리기) 기능을 쉽게 구현할 수 있다. 이런 방식은 명령을 취소하는 코드와 명령을 수행하는 코드가 항상 함께 있게 만든다.

