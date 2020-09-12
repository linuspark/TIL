> 클라이언트가 자신이 사용하지 않는 메소드에 의존 하도록 강제 되어서는 안 된다.
> No client should be forced to depend on methods it does not use.

# 인터페이스 분리 원칙

클라이언트가 자신이 사용하지 않는 메서드에 의존하고 있다면 자신이 사용하지 않는 메서드가 변경됨에 따라 자신 또한 변경이 일어나야만 할 수 있다. 이런 점은 의도하지 않은 결합 때문에 생기는 문제로 인터페이스가 비대화 할 때 주로 발생한다. 때문에 인터페이스를 분리하여 이런 문제를 예방하고자 한다.

# 인터페이스의 오염

A라는 기반 클래스를 상속받아 사용하고 있는 프로그램 모듈 a, b, c가 있다. 여기에 프로그램이 확장되면서 d라는 모듈을 추가하게 되었고 d 라는 모듈은 A 의 함수들 만으로는 원하는 기능을 구현할 수가 없는 문제가 발생하였다. d의 기능을 구현하기 위해 A라는 기반 클래스에 몇몇 함수를 추가하여 A'를 만들어 d 의 기능을 완벽하게 만들 수 있게 되었다.

위 예시에서 A라는 기반 클래스의 인터페이스는 A'로 오염되었다. 여기서 **"오염"**이라는 표현을 사용하는 이유는 모듈 a, b, c 에서는 추가된 함수들을 사용하지 않지만 같은 클래스를 상속받고 있기 때문에 어쩔 수 없이 추가된 함수를 구현해야 하기 때문이다. (추가된 함수에 아무 동작을 하지 않더라도. → LSP를 위반하게 된다.)

상속받아 구현하는 것 이라고 d라는 모듈에 함수를 추가하면 된다고 볼 수는 없다. main은 A라는 클래스 이름으로 a, b, c, d 중 하나를 받아서 사용하고 A.function()와 같은 방법으로 모듈을 실행한다.

# 클래스 인터페이스와 객체 인터페이스

인터페이스를 오염시키지 않으면서 모듈 d 를 구현할 방법으로는 어떤 방법이 있을까?

## 위임하기

기반 클래스 A에서 추가된 ' 라는 부분을 B라고 해 보자. 이 문제를 해결하기 위한 첫 번째 방법으로는 B 라는 인터페이스를 구현하는 클래스 e를 만들고 모듈 d에서는 e를 사용하는 것이다. 

## 다중 상속하기

다중 상속은 이런 문제를 해결하기 위한 일반적인 해결책 이다. 인터페이스 B 를 정의하고 모듈 d가 기반 클래스 A 와 인터페이스 B 를 모두 상속 받는 방식이다. 분리된 인터페이스를 통해 같은 객체를 사용할 수 있는 것이다.

# ATM 의 예시

ATM에서 할 수 있는 각각의 트랜젝션은 Transaction이라는 추상 클래스를 상속받아 생성되었다. 각각의 트랜젝션은 UI의 메소드를 호출하여 각각의 트랜잭션에 맞는 정보를 받아 와야 한다.  UI는 ATM 의 인터페이스가 영어인지 한글인지, 음성인지 점자판 인지에 따라 여러 가지로 구성될 수 있기 때문에 인터페이스로 구현되어 있다.

[TransactionUI](http://www.plantuml.com/plantuml/png/RP3HIWKX48RlVGelYyFn2I8sg61le-Xwqf447SiPsQ1wzzpEmWhhfVmV_-S_4miKgIagU6CfO4NR2CpwkG1nUuPCtqgV7hxGLi6hQ_MhBi0zVcGEqd5Ry1hatHLO8FPPr-gnz8aA95WyMDGlStFfqnD-LcJP37SfLv9ctfDTCGXRzwheavbyBcachju76v3aiPBZ_pMg-uk--JcxlD1vj6x8ZSUEqF7seqSRi_B6tBPpg4F_4Ubwny24v6gAVm00)

DepositTransaction 클래스는 UI 의 RequestDepositAmount 만을 사용할 것이다. 또 TransferTransaction은 ReqeustTransferAmount 만을 사용할 것 이다. UI interface의 다른 함수는 사용하지 않는다. 이런 경우가 ISP에서 이야기하는 비대한 인터페이스가 된다.

만약 새로운 Transaction인 PayGasBillTransaction이 추가되어야 한다면 어떻게 될까? Transaction 을 상속받는 PayGasBillTransaction을 추가하고 이 트랜젝션이 UI 에 요청해야 하는 인터페이스를 UI Interface에 추가한다. 그렇게 되면 DepositTransaction, WithdrawalTransaction, TransferTransaction은 로직 등이 바뀐게 없더라도 UI interface가 변경되었기 때문에 다시 컴파일 되어야 할 것 이다. 

이런 문제를 해결하기 위하여 각 Transaction이 사용하는 UI Interface를 만들고 UI Interface는 개별 트랜젝션의 UI Interface를 다중 상속받아 설계를 고칠 수 있다.

[TransactionISPUI](http://www.plantuml.com/plantuml/png/bP71IWGn38RlVOeUbMNx128hg31NKJpNJeg5cLJRb1NKTxU3moIBGTXZ-__9b_mvLFA5sZmP_rAf-40sJBvM-rWyrlvC6J-DtTrzG6W45vVcs_mQRk4jrqJ2jmhFYLx7uez-afhe6g58nIGaAD47i4z3PzdT0xmtgBGIRkRSa3gP5KOeOk-z8AGoOCnb7h2s65D8W7JVSApBDXA_0l-VGbQ8NK-B-F_yCRQGkAMsLYyHATghh_sOZxZNxgBwz3EfLlLgVpdMkSNlt3KdQHYZEsM2Xa6QbNCnPWFqAPsp9o3noINRrm5mRFFq0m00)

이 경우 새로운 트랜젝션 PayGasBillTransaction이 추가될 경우, 새로운 인터페이스(PayGasBillIUI) 가 생겨나고 UI Interface는 새로운 인터페이스(PayGasBillIUI) 를 추가로 상속 받으면 된다. 새로운 클래스 추가의 충격을 최소화 하는 것이다. 

## 복합체와 단일체

위 예시대로 프로그램이 설계되어 있고 함수 g를 구현해야 한다. 이 때 함수 g는 DepositUI 와 TransferUI를 모두 사용할 수 있어야 한다고 할 때 함수 g를 어떻게 설계해야 할까?

- 복합 인자를 받는 복합체 함수 원형

```csharp
void g(DepositUI depositUI, TransferUI transferUI);
```

- 단일 인자를 받는 단일체 함수 원형

```csharp
void g(UI ui);
```

아마 나라면 깔끔하게 단일체 함수 원형으로 함수를 설계하고 인자를 받을 것 같다. 함수가 깔끔해 보이기도 하고 어차피 UI 인터페이스로 모두 접근할 수 있기 때문이다. 게다가 복합체 함수 원형을 사용할 경우 실제로 함수를 사용할 때 두 인자를 같은 객체를 참조해야 할 것이다. 

```csharp
g(ui, ui);  // 같은 객체를 두 인자로 넣다니..;
```

하지만 대게 복합 형태가 단일 형태 보다는 바람직 하다. UI라는 인터페이스에는 DepositUI와 TransferUI 뿐만 아니라 WithdrawalUI 도 포함되어 있으며 다른 UI가 추가될 여지도 있다. 이런 상황에서 Withdrawal UI 가 변경되는 경우 함수 g는 자신이 사용하지도 않는 함수의 변경사항 때문에 수정이 필요할 수도 있다. 이런 상황은 반갑지 않은 상황이다.

# 결론

비대한 클래스는 클라이언트 간에 이상하고 복잡한 결합도를 만들게 된다. 한 클라이언트가 이 비대한 클래스에 영향을 끼치게 되면 다른 모든 클래스가 영향을 받는 것이다. 따라서 클라이언트는 자신이 호출하는 메소드에만 의존해야 하는데 그렇게 하기 위해 비대한 클래스를 여러가지 인터페이스로 분리해야 하는 것이다 그렇게 하여 호출하지 않는 메서드에 대하여 의존성을 끊고 클라이언트 끼리 서로 독립성을 유지할 수 있다.

---

참고. 로버트C마틴. 클린 소프트웨어 애자일 원칙과 패턴 그리고 실천 방법 (이용원, 김정민, 정지호 옮김)
