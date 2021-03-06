---
layout: entry
title: JAVA 프로그래머를 위한 UML - 3
author: 김성중
author-email: ajax0615@gmail.com
description: 로버트 C. 마틴의 'UML for Java Programmers'를 읽고 정리한 글입니다.
keywords: Java, 자바, UML
publish: true
---

# 7. 실천 방법: dX
여러 개발자가 짧은 시간에 많은 일을 할 수 있도록 돕는 단순한 규칙의 집합을 dX라고 하자.

### 반복적인 개발
dX 핵심은 \'모든 것\'을 \'짧은\' 주기로 반복하는 것이다. 요구사항, 분석, 설계, 구현, 테스팅, 문서화 등 정말 \'모든 것\'이 다 포함된다. 그리고 짧은 주기는 한 주 또는 두 주를 의미한다.

- 최초의 탐사 작업<br/>
요구사항 정의하기.
- 각 기능의 추정치 잡기<br/>
추정치에 대한 단위에 신경을 쓰지 않고, 오직 다른 스토리와 크기를 비교할 수 있는 상대적인 크기에만 주의를 기울인다.
- 스파이크<br/>
이틀이나 사흘 정도 시간을 내서 흥미로운 스토리를 두 세개 간략하게 구현해본다.

### 계획 짜기
계획에서는 단순히 현재 작업 속도로 주기마다 어떤 스토리들을 완수할 수 있을지 파악한다.

- 릴리스 계획하기<br>
가장 중요하고 비용 대비 효율이 높은 스토리들을 고르고, 이 스토리가 릴리스 계획이 된다.
- 반복 주기를 계획하기<br/>
비즈니스 가치가 낮고 비싼 스토리보다 비즈니스 가치가 높고 비용이 싼 스토리를 먼저 골라야 한다. 누군가 개발자에게 태스크를 맡으라고 정하는 것이 아니라, 개발자가 태스크에 스스로 사인한다. 그리고 자신이 사인하는 태스크의 양을 추정하는 것도 개발자에게 맡긴다.
- 중간 지점<br/>
지금까지 완료된 스토리 점수는 끝마친 스토리의 추정치만 모두 더해서 계산한다.
- 결과를 속도에 반영하기<br/>
주기마다 얼마나 많은 스토리 점수를 완수하는지 측정해 보고 다음 주기에는 그만큼만 사인한다. 개인마다 지난번 주기에서 얼마나 많은 인-시간(man-hours) 분량만큼 태스크를 끝마쳤는지 재보고, 다음 주기에는 오직 그만큼만 사인해야 한다.

### 반복 주기를 관리 단계로 조직하기
통합 공정(Unified Process)에 따르면 프로젝트에는 네 가지 관리 단계가 있다. 도입 단계(Inception phase)에서는 시스템이 실행될 수 있는지, 어떤 비즈니스 사례인지 결정하기 위해 노력한다. 정련 단계(Elaboration phase)에서는 시스템의 아키텍처를 결정하고 믿을 수 있는 구현 계획을 작성한다. 구축 단계(Construction phase)에서는 시스템을 구축한다. 마지막으로, 전이 단계(Transition phase)에서는 시스템을 설치하고 사용자와 협력해서 시스템을 조율한다.

통합 공정의 단계마다 반복 주기가 하나 이상 있으며, 주기마다 실제로 작동하는 코드가 결과물로 나온다. 단계가 바뀐다고 프로그래머에게 달라지는 것은 없다. 모든 단계는 비슷한 구조의 반복 주기들로 구성된다. 반복 주기의 구조는 스토리들을 찾아내고, 찾아낸 스토리의 작업량을 추정하고, 어떤 스토리를 구현할지 선택하고, 그것을 구현하는 것이다.

### 반복 주기에서는 어떤 일이 일어나는가
한 번의 반복주기에 우리는 요구사항을 분석하고, 해결 방안을 설계하고, 그 해결 방안을 구현한다. 그리고 관심 범위는 \'스토리들에만\' 한정된다. 다음 주기에 선택될지도 모르는 다른 스토리들을 고려하지 않는다.

이렇게 하면 최고의 아키텍처와 매우 유연한 설계를 얻게 되고 재작업도 아주 적어진다. 우리는 언제나 그 시점에서 가장 중요한 기능을 작업하기 때문이다. 다음 반복 주기에 구현하기로 예정된 기능은, 당연히 지금 작업하는 기능보다 덜 중요하다. 그러므로 우리는 언제나 그때 가장 중요한 것에 주목하는 셈이다.

- 짝은 이뤄 개발하기<br/>
키보드를 다루는 사람은 한 사람일지 몰라도, 지금 무슨 일이 진행 중인지 둘 다 정확하게 알아야 한다.
- 인수 테스트<br/>
선택된 사용자 스토리에 살을 붙여 유스케이스를 만들고 선택한 스토리를 실행해 볼 수 있는 인수 테스트를 작성한다. 이 인수테스트는 주기가 절반 이상 지나기 전에 프로그래머에게 전달된다. 이 인수 테스트야 말로 진정한 요구사항 문서다. 인수 테스트는 보통 쉽게 자동화할 수 있는 고수준의 테스트용 언어로 작성한다.
- 단위 테스트<br/>
단위 테스트를 먼저 만들고, 실제 제품에 들어갈 코드를 작성하는 것이 규칙이다. 실패하는 단위 테스트를 통과하기 위해 작성한 것이 실제 코드의 모든 줄이 된다. 테스트는 문서화의 다른 형식이기도 하다. 특정한 API 함수를 호출하는 방법을 알고 싶다면, 그것을 하는 테스트가 있으니 보면 된다. 어떤 객체를 만드는 방법을 알고 싶다면, 역시 그것을 하는 테스트가 있으니 보면 된다. 테스트는 시스템에 있는 거의 모든 프로그래밍 작업의 예제 모음처럼 사용할 수 있다. 테스트는 뜻이 모호하지 않고, 정확하고, 컴파일할 수도 있으며 실행할 수도 있는 종류의 문서다.
- 리팩터링<br/>
한 무리의 단위 테스트와 인수 테스트의 지원을 받는 한, 우리는 두려움 없이 원하는 대로 무엇이든 변경할 수 있다. 리팩터링이란 시스템의 동작에는 변화 없이 프로그램의 구조만 개선하는 행동을 말한다. 개선 작업은 작은 단계로 나뉘는데, 각 단계가 끝날 때마다 테스트를 돌려 본다.
- 개방된 작업 공간<br/>
서로 자주 상호 작용하며 부담 없이 질문하거나 충고할 수 있고, 책상 옆에 기대어 서서 다른 사람의 코드를 볼 수도 있는 한 팀으로 함께 일하는 것이다.
- 끊임없이 통합 작업<br/>
dx에서는 락을 걸지 않는(nonblocking) 소스 컨트롤 시스템을 사용한다. 이 말은 다른 사람이 체크 아웃했더라도 아무 상관 없이 누구나 모듈을 체크 아웃할 수 있다는 뜻이다. 체크 인을 하기 전 반드시 모든 단위 테스트와 인수 테스트를 통과하는 것을 보여야 한다. 즉, 여러분이 체크인하기 전 반드시 여러분이 변경한 사항을 시스템에 완전히 통합시키고, 시스템을 빌드하고, 테스트해야 한다는 뜻이다.

---

# 8. 패키지
자바 프로그래머에게 중요한 패키지는 두 종류다. 하나는 자바의 package 키워드로 나타내는 소스코드 패키지고, 다른 하나는 .jar 파일로 나타내는 바이너리 컴포넌트다.

자바의 컴파일 시스템은 소스크드의 패키지 구조를 본떠 만든 디렉터리 구조 안에 생성한 이진 .class 파일들을 보관한다. 그리고 .java 파일이 아니라 .class 파일에서 외부 선언을 읽어 오므로, 컴파일러와 런타임 시스템 둘 다 애플리케이션에 포함된 패키지들의 클래스 경로(classpath)를 꼭 올바르게 알아야 한다.

.jar 파일의 형태로 많은 바이너리 코드를 한데 묶어 컴포넌트로 만들고 싶을 때가 있다. 이런 컴포넌트는 여러 시스템에 배포할 때 편리하다.

### 패키지 설계의 원칙
이 원칙에 따라 나뉜 패키지의 목적은 자주 변경하는 클래스를 따로 모으고, 변경할 이유가 다른 클래스를 갈라놓는 것이다. 이 원칙들은 자주 변경하는 클래스와 그렇지 않은 클래스를 분리하려고 노력한다. 또한, 시스템의 고차원 아키텍처를 저차원의 세부사항과 분리하고, 이 고차원 아키텍처를 독립적으로 유지하려고 노력한다.

**패키지 릴리스/재사용 등가 원칙(The Release/Reuse Equivalency Principle, REP)**<br/>
다른 사람들이 편하게 재사용할 수 있는 패키지를 만드는 것도 클래스들을 패키지 안에 배치할 때 고려할 기준이다. 그러므로 재사용할 때 같이 몰려다니는 클래스들을 한 패키지로 묶어놓고, 이것들을 릴리스나 유지보수의 단위로 취급하면 만드는 사람이나 재사용하는 사람 모두 편하다.

**공통 폐쇄 원칙(The Common Closure Principle, CCP)**<br/>
단 하나의 책임 원칙(Single Responsibility Principle, SRP)에 따르면 모든 클래스는 그 클래스를 변경할 이유가 오직 하나뿐이어야 한다. 만약 어떤 것을 변경해야 한다면, 그것 때문에 바꾸어야 할 클래스들이 단 한 패키지에만 몰려 있기를 원한다. CCP의 목표는 변경 가능성이 비슷한 클래스들을 하나로 묶는 것이다. 이렇게 하면, 무엇을 바꿔야 할 경우 의존 관계 구조 안의 패키지들 가운데 매우 적은 수만 변경하면 된다.

**공통 재사용 법칙(Common Reuse Principle, CRP)**<br/>
인터페이스 격리 원칙(Interface Segregation Principle, ISP)에 따르면 클래스의 클라이언트마다 따로따로 인터페이스를 만드는 것이 좋다. 한 클라이언트가 사용하는 클래스들과 다른 클라이언트가 사용하는 클래스들은 최대한 분리해야 한다. 서로 다른 클라이언트가 사용하는 클래스들이 한 패키지에 섞여 있을 경우, 패키지 안의 어떤 클래스를 바꾸면 그 변경된 클래스를 사용하지 않는 패키지들까지 그 변화의 영향을 받을 수도 있다.

**의존 관계 비순환 원칙(Acyclic Dependencies Principle, ADP)**<br/>
패키지 의존 관계 그래프에 순환이 있다면 빌드할 때나 개발할 때 문제가 생길 수도 있다. 순환이 있으면 어떤 클래스와 패키지들을 먼저 빌드하고 어떤 것을 다음에 할지 결정하지 못한다.

**안정된 의존 관계 원칙(Stable Dependencies Principle, SDP)**<br/>
SDP에 따르면 패키지는, 바뀌기 쉬워서 자신보다 불안정한 패키지들에 의존하면 안 된다. 모든 패키지 의존 관계 화살표는 언제나 화살표가 출발하는 패키지(의존하는 패키지)보다 변경하기 어려운 패키지를 가리켜야 한다.

**안정된 추상화 원칙(Stable Abstractions Principle, SAP)**<br/>
개방-폐쇄 원칙(OCP)에 따르면 모듈을 변경하지 않고도 확장할 수 있는 방법이 있다. SAP에 따르면 안정된 패키지를 쉽게 확장할 수 있도록 유지하기 위해, 안정된 패키지는 추상적이어야 한다. 패키지가 안정적일수록 더 추상적이어야 한다. 추상 클래스와 인터페이스의 비율이 높을수록 패키지의 추상도도 높아진다. SDP/SAP 조합에서는 의존 관계를 많이 받아들일수록 안정성도 증가하며, 안정성이 증가하면 추상성도 증가해야 한다고 나와있다. 그러므로 패키지가 의존 관계를 많이 받아들일수록 패키지도 더 추상적이어야 한다.

---

# 9. 객체 다이어그램
시스템의 스냅샷 사진처럼, UML 객체 다이어그램은 어떤 순간의 객체들과 그 객체 사이의 관계 그리고 그 객체들의 속성 값을 보여 준다. 객체 다이어그램은 시스템의 구조를 그 시스템에 속한 클래스의 정적인 구조에서 만들어 내는 것이 아니라 동적으로 만드는 경우 특히 유용하다.

### 어떤 순간의 스냅샷
시스템 내부 구조가 특정 시간에 어떤 모습인지, 또는 시스템이 특정한 상태에서 어떻게 되어 있는지 보일 필요가 있다면 객체 다이어그램이 유용하다. 객체 다이어그램은 설계자의 의도를 보여준다. 그리고 객체 다이어그램은 어떤 클래스들과 관계들이 실제로 어떻게 사용되는지, 또 시스템에 다양한 것이 입력될 때 시스템이 어떻게 변화할지 보여주기도 한다.

하지만 이 다이어그램들은 자주 필요하지는 않으므로, 절대로 시스템에 들어 있는 시나리오마다 이것을 그려야 한다고 생각해서는 안 된다.

---

# 10. 상태 다이어그램
아래 그림은 사용자가 시스템에 로그인하는 방법을 제어하는 상태 기계를 기술하는 \'간단한 상태 전이 다이어그램(State Transition Diagram, STD)\'이다. 이 그림에서 모서리가 둥근 사각형은 \'상태(state)\'를 나타낸다. 사각형을 둘로 나눠 위 부분에 각 상태의 이름을 적고, 아래 부분에는 그 상태에 들어가거나 나갈때 특별히 무엇을 해야 할지 적는다. 예를 들어, 로그인 메시지를 띄우기(Prompting for Login) 상태에 들어갈 때에는 showLoginScreen 행동을 호출한다. 이 상태에 나갈 때에는 hideLoginScreen 행동을 호출한다.

상태 사이의 화살표는 \'전이(transition)\'라고 부른다. 전이마다 그것을 발생시키는 이벤트의 이름이 붙어 있다. 몇몇 전이에는 전이가 일어날 때 수행할 행동이 붙기도 한다. 예를 들어, Prompting for Login 상태에서 로그인 이벤트를 받으면, 사용자가 검증하기(Validating User) 상태로 전이하면서 validateUser 행동도 호출한다.

다이어그램 왼쪽 상단의 검은 동그라미는 \'최초 의사-상태(pseudo state)\'라고 부른다. FSM의 생명은 이 의사 상태에서 전이해 나오며 시작된다. 그러므로 지금 예로 든 상태 기계는 Prompting for Login 상태로 전이해 들어가면서 동작을 시작한다.

![login-state-machine](/images/2019/05/03/login-state-machine.png "login-state-machine"){: .center-image }

비밀번호 보냄 실패(Sending Password Failed) 상태와 비밀번호 보냄 성공(Sending Password Succeeded) 상태를 둘러싼 \'상위 상태(superstate)\'도 하나 그렸는데, 두 상태 모두 똑같이 Prompting for Login 상태로 전이함으로써 OK 이벤트에 반응하기 때문이다. 상위 상태를 사용하면 동일한 화살표를 중복해서 그리지 않아도 되므로 편리하다.

이 유한 상태 기계는 로그인 과정이 어떻게 작동하는지 명확하게 정의한다. 또 이 과정을 작고 간결해서 좋은 함수들로 쪼개 주기까지 한다. 만약 showLoginScreen, validateUser, sendPassword 등의 행동 함수를 모두 구현한 다음, 이 다이어그램에서 보이는 논리 구조로 연결만 하면, 이 로그인 과정이 올바로 작동할 것임을 확신할 수 있다.

### 특수 이벤트
상태 사각형의 아래 부분에는 여러 \'이벤트 / 행동\' 쌍이 들어 있다. 이것 가운데 들어옴(entry) 이벤트와 나감(exit) 이벤트는 표준 이벤트다.

![state-in-uml](/images/2019/05/03/state-in-uml.png "state-in-uml"){: .center-image }

### 상위 상태
비슷한 상태를 둘러싼 상위 상태를 그린 다음, 상태마다 전이 화살표를 그리는 대신 상위 상태에만 그리면 된다. 그러므로 아래 두 다이어그램은 동일하다.

![super-state](/images/2019/05/03/super-state.png "super-state"){: .center-image }

하위 상태에 명시적으로 전이를 그려 넣으면 상위 상태의 전이보다 우선순위가 앞선다. 따라서 아래 그림처럼 S3 상태의 pause 전이가 Cancelable 상위 상태의 기본 pause 전이보다 우선한다. 이렇게 보면 상위 상태가 기반 클래스와 비슷함을 알 수 있다. 유도 클래스가 자기 기반 클래스의 메서드를 재정의(override)하는 것과 마찬가지로 하위 상태는 상위 상태의 전이를 재정의할 수 있다.

상위 상태도 보통 상태처럼 들어옴 이벤트, 나감 이벤트, 특수 이벤트를 가질 수 있다. 위 그림은 상위 상태와 하위 상태 모두 들어옴 행동과 나감 행동이 있는 FSM이다. 어떤 상태(Some state)에서 Sub 상태로 전이되어 들어오면 먼저 enterSuper 행동을 호출하고 그 다음 enterSub 행동을 호출한다. 마찬가지로 FSM 전이가 Sub2에서 어떤 상태(Some State)로 돌아간다면, 먼저 exitSub2를 호출한 다음 exitSuper를 호출한다. 하지만, Sub에서 Sub2로 가는 e2 전이는 상위 상태 바깥으로 나가지 않기 때문에, 단지 exitSub와 enterSub2만 호출한다.

### 최초 의사-상태와 최종 의사-상태
아래 그림에서 UML에서 자주 사용되는 두 의사-상태를 볼 수 있다. FSM의 생명은 최초 의사-상태에서 전이되어 나오는 \'과정\'에서 시작된다. 최초 전이는 이벤트를 가지지 못하는데, 상태 기계 생성이 바로 이 전이를 시작하는 이벤트이기 때문이다. 하지만 행동은 가질 수 있으며, 이 행동이 바로 FSM이 만들어진 다음 곧바로 호출되는 첫 행동이다.

마찬가지로, FSM은 \'최종 의사-상태\'로 전이되는 과정에서 소멸한다. 최종 의사-상태에는 절대로 도달하지 못한다. 만약 최종 의사-상태에 행동이 붙어 있다면, 이 행동은 FSM이 마지막으로 호출하는 행동이 될 것이다.

![initial-final-pseudo-state](/images/2019/05/03/initial-final-pseudo-state.png "initial-final-pseudo-state"){: .center-image }

### FSM 다이어그램 사용하기
다이어그램은 자주 변경해야 하는 시스템을 표현하기에 좋은 매체가 아니다. 반면 글은 변화를 다루기에 아주 유연한 매체다. 그러므로 진화하는 시스템에는 STD보다는 상태 전이 테이블(State Transition Tables, STT)이 좋다.

![subway-std](/images/2019/05/03/subway-std.png "subway-std"){: .center-image }

STT는 열이 네 개 있는 단순한 테이블이다. 테이블의 행 하나는 전이 하나를 나타낸다. 테이블의 한 행을 보면, 전이 화살표의 시작 지점과 끝 지점, 그리고 이벤트와 액션이 모두 들어있다. STT를 읽을 때는 다음 문장을 기본 틀로 삼아서 읽으면 된다. \"만약 Locked(잠김) 상태에서 coin(동전 투입) 이벤트를 받으면, Unlocked(풀림) 상태로 가고, Unlock(풀음) 함수를 호출한다.

![subway-stt](/images/2019/05/03/subway-stt.png "subway-stt"){: .center-image }

---

# References
- [UML 실전에서는 이것만 쓴다: JAVA 프로그래머를 위한 UML](http://www.kyobobook.co.kr/product/detailViewKor.laf?ejkGb=KOR&mallGb=KOR&barcode=9788991268937)
- [UML_for_Java_Programmers](https://www.csd.uoc.gr/~hy252/references/UML_for_Java_Programmers-Book.pdf)
