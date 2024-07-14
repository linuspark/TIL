이 내용은 "애자일 프랙티스" 라는 책을 읽고 내용을 정리한 것이다.

> "무엇을 배우든지 철저히 배우라, 그리하여 네 행동을 타인이 배울 만하게 하라"
 - 타루쿠랄 391절에서 인도의 시인이자 철학자 타루발루바, 기원전 31년

[https://agilemanifesto.org/iso/ko/manifesto.html](https://agilemanifesto.org/iso/ko/manifesto.html)

# 애자일 시작하기

소프트웨어 개발은 머릿속에서 생겨난다. IDE 나 디자인 툴에서 생겨나는 것이 아니다. 머릿속은 생각보다 복잡하기 때문에 태도와 분위기 같은 순간적인 것들이 큰 차이를 만들어 낸다. 이것이 태도에 주의를 기울여야 하는 이유이다. 프로다운 태도란 프로젝트와 팀의 긍정적인 결과, 개인과 팀의 성장, 성공에 집중하는 태도이다. 

애자일은 프로젝트, 일, 경력에 프로다운 태도를 수용할 때에만 작용한다. 바른 태도를 가지고 아래의 실천 방법들을 적용하면 효과를 얻을 수 있다.

- 결과를 위해 일하기

    **비난은 버그를 수정하지 못 한다.** 문제가 발생하였을 때 문제의 해결책을 얻는 것이 중요하지 비난이나 공로를 두고 펼치는 경쟁은 아무런 도움이 되지 못 한다. 

    **프로세스의 준수가 결과는 아니다.** 프로세스를 얼마나 잘 따르는지 재는 것은 결과를 측정하는 것이 아니다. 프로세스보다 결과에 가치를 둔다.

    **균형을 유지하기**

    - 아무 실수도 하지 않는다면 충분히 열심히 일하지 않는 것이다.
    - 결함을 두고 개발자와의 품질 논쟁은 바람직 하지 않다. 보통은 그 문제를 고치는 일이 더 빠르다.
    - 팀원 가운데 한 명이 요구사항, API 호출 등에 대해 오해한다면 다른 팀원도 그럴 수 있다.
    - 한 팀원이 반복해서 잘못된 행동으로 팀에 해를 끼친다면 그 사람은 프로답게 행동하지 않는 것이다. 팀에서 제외하는 것을 고려하라
    - 팀원 대부분이(특히 선도 개발자들이) 프로다운 방식으로 행동하지 않고, 그러 방향으로 나아가는데 관심이 없다면, 그 팀에서 나와서 성공을 추구해야 한다.
- 땜질은 늪을 만든다.

    **버그가 있고, 시간 압박을 받았다.** 땜질을 해도 잘 돌아가는 것 같았다. 다음에 일어나는 일이 좋은 프로그래머와 서투를 해커를 구분한다. 다음에 해야 하는 일은 코드를 남겨두고 다음 문제로 넘어가는 일이 아니라 다른 무언가가 영향을 받는지 이해하고 노력하는 일이다. 

    **지뢰를 조심하라.** 어설픈 수정은 문제를 만들어낸다. 진짜 문제가 무엇인지 모르고 고치는 것은 땜질식 수정이며 지뢰를 해체하지 않고 지나가는 것이다.

    따로 코딩하지 마라. 개발자들이 따로 코딩하지 않게 해야한다. 팀원들은 자신의 동료가 작성한 코드를 볼 수 있는 시간을 가져야 하고 이런 코드 리뷰는 코드를 이해하는데 도움이 될 뿐만 아니라 버그를 찾아내는데 효과적이다.

    단위 테스트를 사용해야 한다. 단위 테스트는 자연스럽게 코드를 다루기 쉽도록 나누어준다. 단위 테스트는 실행 가능한 문서의 일종이다. 이러한 단위 테스트는 코드를 더 작고 이해하기 쉬운 모듈 단위로 볼 수 있게 한다. 

    균형을 유지하기

    - 팀원 가운데 한 사람이 코드가 너무 어려워서 다른 사람은 이해할 수 없다고 말한다면, 누구라도 유지보수 하기가 힘들 것이다.
    - 이해하지 않은 상태에서 코드를 고치는 것을 하지 말아야 한다. 땜질식 수정 증후군은 처음엔 아주 쉽게 시작하지만 급격하게 코드를 알아볼 수 없게 만든다.
    - 대부분의 복잡한 시스템은 너무 난해해서 한 사람이 모든 시스템을 이해하기 어렵다. 작업 중인 특정 부분에 대하여 깊이 이해하는 것 외에도, 시스템의 각 부분들이 어떻게 상호작용 하는지 이해할 필요가 있다.
- 사람이 아니라 생각을 비판하라

    설계에 대한 토의가 과열되어 감정적 충돌이 있을 때 생각 자체가 아니라 그 생각을 말한 사람에 따라서 결정을 내리는 것은 유쾌하지 않은 일이다. 누군가 새로운 설계를 발표할 때 어떻게 말하는가에 따라서 회의가 진행되는 방식이 달라진다.

    - "멍청한 설계잖아" → 무능력 하다는 이유로 오류를 말한 사람을 내쫒는다.
    - "멍청한 설계잖아, 당신은 스레드에 안전하게 설계하는 것은 잊었어" → 명백한 결점을 지적하여 오류가 있는 생각을 기각한다.
    - "고마워, 하지만 동시에 두 명의 사용자가 로그온하면 어떻게 돼?" → 본인의 관심사를 말하기 위해 동료에게 묻는다.

    어떤 방법이 가장 좋은지는 말하지 않아도 알 것이다. 아이디어가 웃음거리가 되거나 창피를 당한다면 실제로 다른 제안을 하지 않으려고 할 것이다. 의견을 말하지 못 하는 분위기야 말로 진짜 문제이다. 

    부정적인 생각은 혁신을 죽인다. 부정적인 언급과 태도는 혁신을 죽인다. 팀에 뛰어난 사람이 한 명 밖에 없는 것은 효율이 떨어질 뿐이지만, 함께 일하기를 거부하며 싸우는 사람이 여럿 있는 것은 효율이 떨어지는 것 보다 더 나쁘다. 비판받는 것을 두려워 하지 말아야 한다. "시작하기 위해 위대할 필요는 없다. 다만 위대해지기 위해 시작해야 한다"(레스 브라운).

- 위험을 무릅쓰고 앞으로 나아가라

    '고양이 목에 방울 달기' 

    다른 사람이 작성한 코드를 수정해야 했을 때, 코드를 이해하기 어렵다고 코드가 얼마나 형편없는지 모두에게 이야기 하고 다니는 것은 카타르시스밖에 느낄 수 없다. 불평일 뿐 해결책이 없는 것이다. 대신 그 코드를 가지고 계속 작업하는 것과 새로 코드를 만드는 것의 장단점을 제시하고 올바를 해결책을 위해 노력하라

    자신이 어떤 컴포넌트를 개발하고 있는 중에 여태껏 잘못된 나무를 오르고 있음을 깨달아 갈아 엎어야 할 때 쟁점을 덮으려고 시도하는 대신 다음과 같이 말하라 "제가 지금껏 한 방식이 올바른 접근방법이 아니라는 것을 깨달았습니다. 그걸 고치기 위해 제가 생각한 방법 몇 가지가 있는데, 또 다른 생각이 있으시면 그것도 듣고 싶습니다. 다만 시간은 더 걸릴 것 입니다." 

    올바른 일을 하라

    - 하늘이 무너질 것 같은 위기 상황인데 팀의 다른 사람들은 동의하지 않는다면, 근거를 충분히 설명하지 못 한 것이다.
    - 하늘이 무너질 것 같은 위기 상황인데 팀의 다른 사람들은 동의하지 않는다면, 그 사람들 말이 맞다고 생각하라
    - 코드 품질을 양보하라는 압력을 받는다면, 개발자로서 회사자산의 품질을 저하시킬 권한이 없다는 사실을 지적하라

# 애자일 기르기

애자일은 자신을 변화에 적응시켜 유지해나갈 것을 요구한다. 소프트웨어 관련 직업은 계속 변화하고 진화하는 분야이다. 계속 페이스를 유지하지 않으면 떨어져 나간다. 대부분의 신기술은 기존의 기술이나 아이디어에 의존하고 있으며 대게는 점진적이다. 게속 좇아간다면 새로운 내용을 배우는 일은 단지 점진적인 변화를 인지하는지 인지하지 않는지에 대한 문제이다.

- 변화에 뒤처지지 말아라

    "변화 외에 영원한 것은 없다." 라고 헤라클레이토스는 말했다. 불행하게도 당장 업무를 하는데 필요한 기술을 가진 것으로는 더 이상 충분하지 않다. 이런 업무는 몇 년 내로 쓸모가 없어져 구식으로 취급될 것 이다. 기술은 끊임없이 발전한다. 그런 기술을 무시하며 지내지 않는다면 갑자기 10층을 오를 필요가 없다. 하지만 새로운 기술을 무시해 왔다면 10층을 한 꺼번에 올라야 하기 때문에 숨이 차오른다. 기술 발전의 속도를 따라가기 위하여 다음과 같은 방법을 제시한다.

    - 반복해서 조금씩 배우자 - 신기술을 따라잡는데 매일 일정한 시간을 투자한다. 공부시간이 길 필요는 없다 규칙적이면 된다.
    - 최신 소식을 얻자 - 포럼의 토론을 읽거나 메일링 리스트를 구독하거나 기술 블로그를 규칙적으로 읽는다.
    - 지역 사용자 그룹에 참석하자 - 다양한 기술 영역에 사용자 그룹이 존재한다. 사용자 그룹에 참석하여 연설을 듣고 질문과 답변시간에 참석한다
    - 워크숍이나 학회에 참석하자 - 컴퓨터 학회는 전 세계적으로 열린다. 전문가에게 직접 배울 수 있는 기회이다.
    - 열심히 읽자 - 좋은 책을 찾아보되 소프트웨어 개발, 비 기술적 주제, 저널, 대중매체의 출판물 등을 다양하게 읽는다.

    균형 유지하기

    - 모든 것에 전문가가 될 수는 없다. 그렇게 되려고 하지 마라. 하지만 일단 몇 가지 분야에 전문가가 된다면 선택한 새 분야에서 전문적인 지식을 얻는 것이 쉬워진다.
    - 신기술이 왜 필요한지 이해하라. 무슨 문제를 해결하고 어디에 쓰일 수 있는것인지 이해하여라
    - 새 기술을 배운다고 바로 어플리케이션을 새 기술이나 프로그래밍 언어로 바꾸려는 충동을 삼가라
- 팀에 투자하라

    팀에는 다양한 능력과 경험과 기량을 가진 개발자가 있다. 사람마다 역량과 전문 분야가 다르며 이런 재주와 배경이 다양하게 조합되어 학습하기 이상적인 환경이 탄생한다. 팀에서 혼자 많이 아는 것으로는 충분하지 않다. 교육이 더 잘 된 팀이 더 좋은 팀이다.

    '도시락 회의' 는 팀에서 지식을 공유하는 좋은 방법이다. 일주일 중에 하루, 예를 들어 수요일에 점심을 같이 하는 계획을 세워서 매 주 한명씩 회의를 이끌게 한다. 토의를 이끄는 사람은 개념을 제시하거나 툴 사용법, 팀의 관심을 끄는 무엇인가를 소개한다. 뭐든지 도움이 될 만한 것을 하는 것이다.

    균형 유지하기

    - 단원별로 책을 한 권 읽는 독서모임은 유용하지만 좋은 책을 골라야 한다. "디자인 패턴과 UML 일주일 완성" 과 같은 책은 좋은 책이 아니다.
    - 모든 주제가 성공적일 수는 없다. 시점이 적절하지 않을 수도 있다. 어찌되었든 주의를 기울이자. 노아가 방주를 지을 때에도 비가 오고 있었던 것은 아니다.
    - 팀 내로 회의를 한정한다. 팀원간의 친밀함을 쌓고 토론할 기회를 가지는 것이 중요하다.
    - 규칙적인 일정을 지켜라. 일정하고 작은 규모의 접촉이 애자일한 것이다.
    - 순수하게 기술적인 책이나 주제 너머로 확장하자
    - 도시락 회의는 설계회의가 아니다. 특정한 쟁점을 해결하는 것은 설계회의로 넘기는 것이 낫다.
- 버려야 할 때가 언제인지 알자

    애자일의 기초 중 하나는 변화에 익숙해지는 것 이다. 변화가 빈번하다면 기존에 쓰던 기술이나 툴을 쓰는 것이 말이 될까? 내가 익숙한 것 이라도 "버릴"수 있는 필요성을 생각해야 한다. 

    대가를 많이 치른 사고방식은 쉽게 버릴 수 없다. 오래된 습관은 바꾸기 힘들고 그 습관을 알아차리는 것도 힘이 든다. 내가 구식의 접근방식을 사용한다는 것을 깨달아야 한다.

- 이해할 때까지 질문하라

    문제를 잘 해결하기 위해서는 큰 그림을 이해해야 한다. 다른사람이 어떻게 생각하든지, 관계되었다고 생각하는 모든 부분을 살필 필요가 있다. "왜 그래요?" 라고 묻는 것은 휼륭한 질문이다. 단순한 증상이 아니라 진짜 문제가 무었인지 알게된다.

    균형 유지하기

    - 핵심에서 완전히 벗어난 질문을 할 수도 있다. 관련된 질문을 하도록 하자
    - "왜 그래요?" 라고 물을 때, "왜 질문하는데요?" 라고 반대로 질문을 받을 수도 있다. 질문을 할 때 질문의 타당성을 항상 간직해야 한다.
    - 피상적인 답은 받아들이지 말아라. "항상 그렇게 해왔어요" 와 같은 대답은 대답이 아니다.
- 리듬을 느끼라

    별로 성공적이지 못한 많은 프로젝트에서 발생하는 사건들은 불규칙하고 우연하게 발생한다. 그리고 그렇게 발생하는 위협에 대처하는 것은 쉽지 않다. 내일 무슨 일이 생길 지 모르기 때문이다. 애자일 프로젝트에서는 리듬과 주기가 있어서 편안해진다. 스크럼 같은 경우 스프린트 동안 요구사항 변화로부터 팀을 보호한다. 큰 규모의 변화는 따로 구분하여 한꺼번에 다룬다.

    타임박싱(Time Boxing) : 연장할 수 없는 활동에 대한 확고하고 짧은 마감. 마감은 항상 고정되어야 한다. 전체 일을 끝내기 위한 얼마나 많은 타임박싱이 있어야 하는지는 모르겠지만 각각의 박스는 짧게 한정되고 명확한 목표를 달성한다. 종료날짜는 바꿀 수 없지만 기능은 뺄 수 있다. 

    일이 쌓이기 전에 부딪쳐라. 사건들 사이에 꾸준하고 반복적인 간격을 유지해야 일상적으로 되풀이되는 일을 해결하기 쉽다. 

    균형 유지하기

    - 하루 일과가 끝날 때 까지 모든 코드를 남김없이 체크인하고 테스트하도록 하루를 계획하라
    - 마무리 하느라 야근하지 마라
    - 팀의 반복기간을 고정하고 규칙적이게 하라
    - 규칙적인 리듬이 너무 강렬하면 기력이 소진된다. 일반적으로 팀 외부나 조직 외부의 대상과 교류할 때에는 더 느린 리듬을 적용한다.
    - 다이어트 할 때 조금만 성공하더라도 큰 동기부여가 되는 것 처럼, 작지만 도달할 수 있는 목표를 세우면 모든 사람이 앞으로 나갈 수 있다. 그리고 작은 성공을 축하하라.
	
# 사용자가 원하는 내용을 제공하기

고객의 요구사항을 전달받고 애플리케이션을 구현하여 제공하면 대부분의 사용자들은 원래 제공한 사양(요구사항) 외의 기능을 요구한다. 고객이 요구사항을 전달할 때에는 고객도 자신의 요구사항이 어떤 것인지 명확하게 이해하고 있지 않기 때문에 어플리케이션이 완성되면서 요구사항은 조금씩 바뀌기 마련이다.

- 고객이 결정하도록 하라

    어떤 작업을 수행하는데 두 가지 구현 방법이 있다고 하자. 첫 번째 방법은 빠르지만 사용자가 할 수 있는 기능을 제약한다. 두 번째 방법은 시간이 더 걸리지만 사용자에게 유연선을 준다. 분명 시간의 압박을 받고 있으니 더 빠른 첫 번째 옵션으로 가야하는가? 어떻게 결정해야 할까?

    **결정하지 말아야 할 것을 결정하라**. 개발자와 관리자가 수행하는 가장 중요한 설계 결정은 무엇이 자신의 권한 밖인지 정하고 그 이슈를 사업주가 정하도록 하는 것이다. 가능한 선택 사항을 준비하고 장단점을 제시하라. 예상 비용과 이읷에 대해서 기술적인 이슈 대신 사업적인 관점에서 보여준다. 

    균형 유지하기

    - 결정과 그 근거에 대해서 기록을 남긴다. 위키나 메일 이력, 이슈 추적등 무엇이든 상관 없다
    - 비지니스에 영향이 없으면 낮은 수준의 세부사항이다. 이런것은 직접 결정한다.
- 설계가 강요하는 대신 안내하도록 하라

    말하는 대상을 알지 못 하고 그 대상에 정확해질 수 없다. - 요한 폰 노이만

    설계를 매우 상세하게 해서 '코더'가 그대로 구현만 할 수 있도록 하는 것은 여러가지 문제를 발생시킬 수 있다. 프로그램이 완성되어 가면서 새로 알 수 있는 내용들이 있기 때문이다. 설계는 구현하는데 필요한 만큼만 상세해야 한다. 

    전략적 설계와 전술적 설계. 선행하는 전략적 설계는 매서드, 매개변수, 필드 등의 상세 세부내용이나 객체간의 상호작용에 대한 정확한 순서에 대한 세부내용을 명시하면 안된다. 이런 세부내용들은 전술적 설계에 맡겨야 한다. 좋은 전략적 설계는 올바른 방향을 가리키는 지도와 같은 역할을 한다. 

    균형 유지하기

    - "미리 대규모 설계를 할 수 없다" 라는 말은 설계가 전혀 없다는 말이 아니다. 실제 코드로 검증하는 일 없이 설계작업에 매달리지 말라는 뜻이다. 설계에 대한 고민 없이 코딩에 뛰어드는 것은 위험하다.
    - 초기 설계가 쓸모없는 것으로 결론이 나도 초기 설계는 해야한다. 설계를 만드는 행동은 그 행동으로써 가치가 있다.
- 기술 사용을 정당화 하라

    프레임워크를 무턱대고 고르는 것은 세금을 줄이려고 아이를 갖는 것과 같다. 새로운 기술이나 프레임 워크에 대해 생각하기 전에 해결하려는 문제가 무엇인지 확인해야 한다. 기술을 쓰면 멋있고 프로그래머의 솜씨를 향상시킬 것 같은 '이력서 주도 설계'를 지양해야 한다. 

    - 새로운 기술이 문제를 정말로 해결하는가? - 필요하다면 프로토타입을 작성하라
    - 이 새로운 기술에 얽매이게 되는가? - 어느정도 개방적인지, 독점적인지 고려하여야 한다.
    - 유지보수 비용은 어떠한가? - 해결책이 문제보다 더 싸야지 그렇지 않으면 잘못된 투자이다.

    사용을 고려하고 있는 프레임워크(또는 기술)를 검토할 때 그 기술이 제공하는 다양한 기능에 끌린것은 아닌지, 발견한 해결책에 맞는 문제를 찾은것은 아닌지 확인해야 한다. 이것은 충도구매자가 계산대에서 물건을 더 사는 행동과 비슷하다.

    **다운로드해 얻을 수 있는 프로그램을 새로 만들지 마라.** 코딩을 적게 할수록 유지보수 할 양이 줄어든다. 

    균형 유지하기

    - 모든 기술에는 장단점이 있다. 그 기술이 오픈소스이건 상용 제품이건 프레임워크건 툴이건 언어건 간에 그 기술에 따라오는 장단점을 알아야 한다.
    - 즉시 다운로드 할 수 있는 것을 새로 만들지 말아라. 밑바닥부터 필요한 모든 것을 만드는 것이 불가피할 수도 있지만 그것은 제일 비싼 선택이다.

- 코드를 릴리즈할 수 있게 유지하라

    체크인한 코드는 항상 바로 쓸 수 있어야 한다. 팀에서 일할 때 자신이 만든 변경 사항에 민감해야 하고, 자신이 시스템의 상태와 팀 전체의 생산성에 영향을 준다는 사실을 계속 명심해야 한다. 망가진 코드를 체크인 하지 않기 위해서 다음과 같은 업무 흐름을 가져갈 필요가 있다.

    - 로컬 테스트를 실행하여라 - 작업한 코드가 컴파일 되고 모든 단위테스트를 통과하는 것을 확인하고 시작하고 끝낼 때에도 모든 테스트가 통과되는 것을 보고 끝내라
    - 최신 소스를 체크아웃 하여라 - 소스코드의 최신 버전을 가져와서 그것으로 컴파일 하고 테스트 하여라
    - 체크인 해라 - 변경사항을 로컬에만 두지 말고 저장소에 체크인 해라

    아주 간단하고 당연한 업무 흐름이지만 그만큼 무시하기도 쉬운 것들이다. 지속적 통합 시스템을 이용하여 계속해서 테스트하여라. 그리하여 프로젝트를 항상 컴파일 할 수 있고 실행할 수 있으며, 테스트하고 당장 배치할 수 있게 하여야 한다. 

    균형 유지하기

    - 시스템이 릴리즈 할 수 없는 상태로 있는 기간을 늘여야 한다면 브랜치 버전을 만들어서 실험하여라. 시스템을 릴리즈 할 수 없으면서 동시에 되돌릴 수 없게 만들지 말아야 한다.
- 일찍, 자주 통합하라

    애자일의 주요 특징은 일시적이 아닌 지속적인 개발이다. 특히 이러한 점은 다른 팀원들이 작업한 코드와 통합할 때 필요하다. 통합한다는 것은 생각보다 많은 노력이 필요하다. 그것은 통합을 미루면 미룰수록 더 커지는 종류의 노력이다. 통합은 제품 개발에서 주요 위험 분야의 하나이기 때문에 서브 시스템이 통합되지 않은 채 커지도록 놔두면 더 근 위험에 노출되게 된다. 

    통합과 격리는 상호 배타적인 것이 아니다. 모의 객체(Mock object)를 이용하면 코드를 의존성에서 분리하여 통합 전에 테스트 할 수 있다.

    대규모 통합을 받아들이지 말아야 한다. 일찍 통합함으로써 어떻게 서브시스템들이 상호작용하고 동작하는지 알 수 있다. 

    균형 유지하기

    - 성공적인 통합은 모든 단위테스트를 계속 통과하는 것을 의미한다. "우선 해를 끼치지 말라"
    - 코드를 자주 통합하지 않으면 코드를 작성하는 대신에 코드를 통합하는 데서 발생한 문제에 시간을 다 뺏길 수 있다. 통합할 때 문제가 많다면 충분히 자주 통합하지 않은 것이다.
    - 너무 오래 격리해 있지 말고 일단 경험에서 배운 뒤에 통합을 향해 빨리 나아가라.

- 일찍, 자주 통합하라

    애자일의 주요 특징은 일시적이 아닌 지속적인 개발이다. 특히 이러한 점은 다른 팀원들이 작업한 코드와 통합할 때 필요하다. 통합한다는 것은 생각보다 많은 노력이 필요하다. 그것은 통합을 미루면 미룰수록 더 커지는 종류의 노력이다. 통합은 제품 개발에서 주요 위험 분야의 하나이기 때문에 서브 시스템이 통합되지 않은 채 커지도록 놔두면 더 근 위험에 노출되게 된다. 

    통합과 격리는 상호 배타적인 것이 아니다. 모의 객체(Mock object)를 이용하면 코드를 의존성에서 분리하여 통합 전에 테스트 할 수 있다.

    대규모 통합을 받아들이지 말아야 한다. 일찍 통합함으로써 어떻게 서브시스템들이 상호작용하고 동작하는지 알 수 있다. 

    균형 유지하기

    - 성공적인 통합은 모든 단위테스트를 계속 통과하는 것을 의미한다. "우선 해를 끼치지 말라"
    - 코드를 자주 통합하지 않으면 코드를 작성하는 대신에 코드를 통합하는 데서 발생한 문제에 시간을 다 뺏길 수 있다. 통합할 때 문제가 많다면 충분히 자주 통합하지 않은 것이다.
    - 너무 오래 격리해 있지 말고 일단 경험에서 배운 뒤에 통합을 향해 빨리 나아가라.

- 배치를 일찍 자동화 하라

    품질 보증에서는 배치를 테스트 해야 한다. 품질보증을 위한 애플리케이션 설치 중 이라면 시간이 조금 더 들더라도 그 과정을 자동화 하여라. 일찍 자동화를 시작함으로써 애플리케이션 설치 절차를 테스트 할 기회를 얻게 된다. 프로젝트 생해 동안 의존관계에 있는 변화를 따라가는 일이 더 쉬워진다. 컴포넌트가 빠졌거나 라이브러리가 호환되지 않는 문제를 보다 일찍 발견할 수 있다.

- 데모를 사용하여 자주 피드백을 받아라

    요구사항은 잉크처럼 유동적이다. 프로젝트의 시작 전에 고객이 견고하고 잘 정의된 요구사항을 준다고 기대한다면 크게 실망할 것 이다. 고객의 생각과 기대는 내용을 말 한 후에도 계속해서 진화하는데, 특히 새 시스템의 일부를 사용하고 시스템의 영향력과 가능성을 확인 한 후에는 더욱 그렇다. 고객의 요구를 받을 때와 개발한 내용을 보여줄 때의 시간 간격이 클 수록 고객의 기대에서 멀어진다.

    피드백을 자주 받아라. 반복 주기가 매 분기나 매 년 이라면 주간이나 격주로 줄여라. 

    균형 유지하기

    - 고객과 함께 일하는 방식을 처음으로 제안할 때 고객은 너무 '릴리즈' 가 많다고 생각할 수 있다. 이런 '릴리즈' 는 내부 릴리즈 이며 전체 사용자 집단을 위한 것이 아니라는 사실을 이해시켜야 한다.
    - 고객이 피드백을 주고 프로젝트의 방향을 조정하는 것에 데모의 목적이 있다. 기능이나 안정성이 부족하여 고객을 동요시키거나 화나게 해서는 안된다. 안전성이 없으면 보여주지 말아야 한다. 기능에 대한 기대를 명확하게 정해야 한다. 즉, 고객이 보고 있는 애플리케이션은 개발중이며, 최종 완성 제품이 아니라는 사실을 알게 하여야 한다.

- 짧은 반복을 사용하여, 점진적으로 배포하라

    통합 프로세스와 애자일 방법론은 모두 반복적이고, 점진적으로 개발하라고 이야기한다. 대부분의 사용자 들은 일 년 후 더 좋은 소프트웨어를 기다리느니 당장 좋은 소프트웨어를 갖고 싶어한다.(실용주의 프로그래머:적당히 괜찮은 소프트웨어) 제품을 쓸모있게 만드는 핵심 기능이 무엇인지 확인하고 그 기능을 실제 고객의 손에 가능한 빨리 제공하는 것을 목표로 한다. 

    **최소의 유용한 기능 단위로 묶어서 제품을 릴리즈하라.** 각 투가기능의 개발에 1~4주 정도의 반복 주기를 사용하여라

    균형 유지하기

    - **적절한 반복 주기를 정하는 일이 균형을 잡는데 결정적이다**. 반복의 길이가 정확히 4주여야 한다고 확고히 믿는 고객이 있었고 그 속도에 맞추다보니 팀이 죽어나갈 지경이었다. 코드를 개발하지 못 하고 유지보수에만 전념해야 했다. 이 상황의 해결책은 일주일의 유지보수 업무와 그 후 다음 반복을 시작하는 업무로 분리하는 것 이었다. 반복이 꼭 이어져야 한다는 법은 없다.
    - 반복마다 충분한 시간이 없다면, 업무가 너무 많거나 반복이 너무 짧은 것이다.
    - 점진적인 릴리즈는 사용할 수 있어야 하고 고객에게 가치를 제공해야 한다. 고객이 중요하게 여기는 가치는 짐작하지 말고 직접 물어보라
	
- 고정 가격은 깨진 약속이다.

    소프트웨어 프로젝트의 변덕스럽고 재생 불가능한 본질 때문에 미리 고정가격을 들고 나오는 것은 일하는 도중에 깨진 약속이 될 것이 뻔하다. 

    균형 유지하기

    - 계획에 기초한, 애자일하지 않은 환경에서 개발한다면 그런 환경에 맞는 개발 방법론을 고려하던지 아니면 환경을 바꾸어라
    - 애자일 하다는 말이 "일단 코딩을 시작하고 일은 끝난 다음 알게 된다" 는 것을 의미하지 않는다. 현재 지식과 가정 아래에서 어떻게 그렇게 견적을 냈는지, 오차의 폭은 어느정도 인지 설명과 함께 대략적인 견적을 낼 필요는 있다.
	
# 애자일 피드백

애자일 프로젝트에서는 작고 많은 변경 사항들을 지속적으로 조정하기 위해서 많은 피드백을 요구한다. 이런 피드백을 어떻게 얻을 수 있을까? 

- 수호천사를 곁에 두기

    코드는 빠르게 변화한다. 애자일은 변화를 관리하는 것이고 아마도 가장 많이 변하는 것은 코드 일 것 이다. 코드의 변화에 대처하기 위해서는 코드의 건강함이 우선 되어야 할 것이고 코드의 건강함을 측정하고 유지하기 위해서는 자동화 된 단위 테스트가 필요하다. 

    코딩 피드백. 단위 테스트는 널리 보급되어진 애자일 실천 방법 중에 하나이다.

    - 단위 테스트로 즉각적인 피드백을 받기
    - 단위 테스트로 코드를 강하게 만들기
    - 단위 테스트를 디자인 툴로 사용하기
    - 단위 테스트로 자신감 향상시키기
    - 단위 테스트는 믿을만한 문서가 될 수 있다.
    - 단위 테스트를 학습 도우미로 활용하기

- 만들기 전에 사용하라

    "자신이 만든 개밥을 스스로 먹자" 스스로 만든 제품을 최고로 만들기 위해서는 스스로 제품을 적극적으로 사용해야 한다.

    개발자는 API를 만들고 호출하고 인터페이스를 사용하는 일을 하기 때문에 인터페이스를 사용해 보고 배포해야 한다. 더 나아가서 개발하기 전에 그 인터페이스를 사용할 수 있어야 한다. 

    코드를 작성하기 전에 테스트 하기. TDD라고 알려진 기술을 사용한다면 코드를 구현하기 전에 사용할 수 있다. 테스트를 작성하는 것은 구현하는 관점이 아닌 사용하는 관점에서 작성해야 하기 때문이다.

    좋은 디자인이 더 많은 클래스를 뜻하지는 않는다. 객체지향 시스템을 설계하고 개발할 때 대체적으로 객체를 사용한다고 생각할 수 있다. 진짜로 클래스가 필요하지 않은 경우에도 말이다. TDD를 이용한다면 코드를 작성하기 전에 어떻게 사용할 지 고민하기 때문에 더 실용적인 설계에 도달할 수 있다.

    균형 유지하기

    - 테스트 우선이냐 코드 작성 후 테스트냐에 사로잡히지 말자. 테스트 우선은 설계를 개선하지만 코드 작성 후에도 항상 테스트를 해야한다.
    - 모든 설계는 향상될 수 있다.
    - 단위테스트 만으로는 더 나은 디자인을 보장하지는 않지만 더 쉬운 디자인을 만들 수 있다.
