---
layout: entry
title: 클린 아키텍처(Clean Architecture) 2
author: 김성중
author-email: ajax0615@gmail.com
description: 클린 아키텍처(Clean Architecture)를 읽고 정리한 글 입니다.
keywords: 클린 아키텍처, Clean Architecture
publish: true
---

![Clean Architecture](/images/2019/10/26/clean_architecture.JPG "Clean Architecture"){: .center-image }

# 15장. 아키텍처란?
아키텍처의 주된 목적은 시스템의 생명주기를 지원하는 것이다. 좋은 아키텍처는 시스템을 쉽게 이해하고, 쉽게 개발하며, 쉽게 유지보수하고, 또 쉽게 배포하게 해준다. 아키텍처의 궁극적인 목표는 시스템의 수명과 관련된 비용은 최소화하고, 프로그래머의 생산성은 최대화하는 데 있다.

### 개발
시스템 아키텍처는 개발팀(들)이 시스템을 쉽게 개발할 수 있도록 만들어야만 한다. 일례로 팀이 개발자 다섯명으로 구성될 정도로 작다면, 잘 정의된 컴포넌트나 인터페이스가 없더라도 서로 효율적으로 협력하여 모노리틱 *monolithic* 시스템을 개발할 수 있다. 다른 한편으로 일곱 명씩 구성된 총 다섯 팀이 시스템 개발을 한다면 이 시스템의 아키텍처는 다섯 개의 컴포넌트(각 팀마다 하나씩) 발전될 가능성이 높다.

### 배포
소프트웨어 아키텍처는 시스템을 단 한 번에 쉽게 배포할 수 있도록 만드는 데 그 목표를 두어야 한다.

### 운영
시스템 아키텍처는 유스케이스, 기능, 시스템의 필수 행위를 일급 *first-class* 엔티티로 격상시키고, 이들 요소가 개발자에게 주요 목표로 인식되도록 해야 한다. 이를 통해 시스템을 이해하기 쉬워지며, 따라서 갭라과 유지보수에 큰 도움이 된다.

### 유지보수
유지보수는 모든 측면에서 봤을때 비용이 가장 많이 든다. 시스템을 컴포넌트로 분리하고, 안정된 인터페이스를 두어 서로 격리한다. 이를 통해 미래에 추가될 기능에 대한 길을 밝혀 둘 수 있을 뿐만 아니라 의도치 않은 장애가 발생할 위험을 크게 줄일 수 있다.

### 선택사항 열어 두기
소프트웨어를 부드럽게 유지하는 방법은 **중요치 않은 세부사항** 을 가능한 많이, 그리고 가능한 한 오랫동안 열어두는 것이다.

아키텍트의 목표는 시스템에서 정책을 가장 핵심적인 요소로 식별하고, 동시에 세부사항은 정책에 무관하게 만들 수 있는 형태의 시스템을 구축하는데 있다. 이를 통해 세부사항을 결정하는 일은 미루거나 연기할 수 있게 된다.

- 개발 초기에는 데이터베이스 시스템을 선택할 필요가 없다.
- 개발 초기에는 웹 서버를 선택할 필요가 없다.
- 개발 초기에는 REST를 적용할 필요가 없다.
- 개발 초기에는 의존성 주입 *dependency injection* 프레임워크를 적용할 필요가 없다.

 세부사항에 몰두하지 않은 채 고수준의 정책을 만들 수 있다면, 이러한 세부사항에 대한 결정을 오랫동안 미루거나 연기할 수 있다. 이를 통해 다양한 실험을 시도해볼 수 있는 선택지도 열어 둘 수 있다.

---

# 16장. 독립성

### 유스케이스
좋은 아키텍처가 행위를 지원하기 위해 할 수 있는 일 중에서 가장 중요한 사항은 행위를 명확히 하고 외부로 드러내며, 이를 통해 시스템이 지닌 의도를 아키텍처 수준에서 알아볼 수 있게 만드는 것이다.

### 운영
시스템의 운영 지원 관점에서 볼 때 아키텍처는 더 실질적이며 덜 피상적인 역할을 맡는다. 시스템이 초당 100,000명의 고객을 처리해야 한다면, 아키텍처는 이 요구와 관련된 각 유스케이스에 걸맞은 처리량과 응답시간을 보장해야 한다.

### 개발
각 팀이 독립적으로 행동하기 편한 아키텍처를 만들려면 잘 격리되어 독립적으로 개발 가능항 컴포넌트 단위로 시스템을 분할할 수 있어야 한다.

### 배포
좋은 아키텍처는 즉각적인 배포 *immediate deployment* 가 가능해야 한다. 시스템이 빌드된 후 즉각 배포할 수 있도록 지원해야 한다.

### 선택사항 열어두기
좋은 아키텍처는 선택사항을 열어 둠으로써, 향후 시스템에 변경이 필요할 때 어떤 방향으로든 쉽게 변경할 수 있도록 한다.

### 계층 결합 분리
아키텍트는 필요한 모든 유스케이스를 지원할 수 있는 시스템 구조를 원하지만, 유스케이스 전부를 알지는 못한다. 따라서 아키텍트는 단일 책임 원칙과 공통 폐쇄 원칙을 적용하여, 그 의도의 맥락에 따라서 다른 이유로 변경되는 것들은 분리하고, 동일한 이유로 변경되는 것들은 묶는다.

업무 규칙은 그 자체가 애플리케이션과 밀접한 관련이 있거, 혹은 더 범용적일 수도 있다. 예를 들어 입력 필드 유효성 검사는 애플리케이션 자체와 밀접하게 관련된 업무 규칙이다. 반대로 계좌의 이자 계산이나 재고품 집계는 업무 도메인에 더 밀접하게 연관된 업무 규칙이다. 이들 서로 다른 두 유형의 규칙은 각자 다른 속도로, 그리고 다른 이유로 변경될 것이다. 따라서 이들 규칙은 서로 분리하고, 독립적으로 변경할 수 있도록 만들어야만 한다.

### 유스케이스 결합 분리
시스템에서 서로 다른 이유로 변경되는 요소들의 결합을 분리하면 기존 요소에 지장을 주지 않고도 새로운 유스케이스를 계속해서 추가할 수 있게 된다.

### 결합 분리 모드
유스케이스와 계층 결합을 제대로 분리했다면 운영 중인 시스템에서도 계층과 유스케이스를 교체 *hot-swap* 할 수 있다. 새로운 유스케이스를 추가하는 일은 시스템의 나버지는 그대로 둔 채 새로운 jar 파일이나 서비스 몇 개를 추가하는 정도로 단순한 일이 된다.

### 중복
예를 들어 두 유스케이스의 화면 구조가 매우 비슷하다고 가정해보자. 이는 우발적 중복일 가능성이 높다. 시간이 지나면서 두 화면은 서로 다른 방향으로 분기하며, 결국에는 매우 다른 모습을 가질 가능성이 높다. 이러한 이유로, 해당 코드를 통합하지 않도록 유의해야 한다.

### 결합 분리 모드(다시)
계층과 유스케이스의 결합을 분리하는 방법은 다양하다.

- **Source level**: 소스 코드 모듈 사이의 의존성을 제어할 수 있다. 이를 통해 하나의 모듈이 변하더라도 다른 모듈을 변경하거나 재컴파일하지 않도록 만들 수 있다.
- **Deployment level**: jar 파일, DLL, 공유 라이브러리와 같이 배포 가능한 단위들 사이의 의존성을 제어할 수 있다. 이를 통해 한 모듈의 소스 코드가 변하더라도 다른 모듈을 재빌드하거나 재배포하지 않도록 만들 수 있다.
- **Service level**: 의존하는 수준을 데이터 구조 단위까지 낮출 수 있고, 순전히 네트워크 패킷을 통해서만 통신하도록 만들 수 있다. 이를 통해 모든 실행 가능한 단위는 소스와 바이너리 변경에 대해 서로 완전히 독립적이게 된다(예, 서비스 또는 마이크로서비스).

컴포넌트가 서비스화될 가능성이 있다면 나는 컴포넌트 결합을 분리하되 서비스가 되기 직전에 멈추는 방식을 선호한다.

좋은 아키텍처는 시스템이 모노로틱 구조로 태어나서 단일 파일로 배포되더라도, 이후에 독립적으로 배포 가능한 단위들의 집합으로 성장하고, 또 독립적인 서비스나 마이크로서비스 수준까지 성장할 수 있도록 만들어져야 한다.

---

# 17장. 경계: 선 긋기
프레임워크, 데이터베이스, 웹 서버, 유틸리티 라이브러리, 의존성 주입에 대한 결정 등을 포함한 유스케이스와 관련이 없는 시스템의 업무 요구사항을 너무 일찍 결정하면 **결합** *coupling* 을 만든다. 그리고 이는 인적 자원의 효율을 떨어뜨리는 요인이 된다.

### 어떻게 선을 그을까? 그리고 언제 그을까?
관련이 있는 것과 없는 것 사이에 선을 긋는다. GUI는 업무 규칙과는 관련이 없기 때문에, 이 둘 사이는 반드시 선이 있어야 한다.

업무 규칙은 스키마, 쿼리 언어, 또는 데이터베이스와 관련된 나머지 세부사항에 대해 어떤 것도 알아서는 안된다. 업무 규칙이 알아야 할 것은 데이터를 가져오고 저장할 때 사용할 수 있는 함수 집합이 있다는 사실이 전부다. 이러한 함수 집합을 통해서 우리는 데이터베이스를 인터페이스 뒤로 숨길 수 있다.

![인터페이스 뒤로 숨은 데이터베이스](/images/2019/11/05/17_1.png "인터페이스 뒤로 숨은 데이터베이스"){: .center-image }

경계선은 상속 관계를 횡단하면서 DatabaseInterface 바로 아래에 그어진다(그림 17.2).

![경계선](/images/2019/11/05/17_2.png "경계선"){: .center-image }

DatabaseAccess에서 출발하는 두 화살표는 모두 바깥쪽으로 향한다. DatabaseAccess가 존재한다는 사실을 알고 있는 클래스는 없다는 뜻이다.

![업무 규칙과 데이터베이스 컴포넌트](/images/2019/11/05/17_3.png "업무 규칙과 데이터베이스 컴포넌트"){: .center-image }

Database 컴포넌트는 BusinessRule 컴포넌트에 대해 알고 있다. BusinessRule는 Database에 관해 알지 못한다. 두 컴포넌트 사이에 이러한 경계선을 그리고 화살표의 방향이 BusinessRule를 향하도록 만들었으므로, BusinessRule에서는 어떤 종류의 데이터베이스도 사용할 수 있음을 알 수 있다. Database 컴포넌트는 다양한 구현체로 교체될 수 있으며, BusinessRule는 조금도 개의치 않는다.

### 입력과 출력은?
예를 들어, 비디오 게임에서 화면, 마우스, 버튼, 음향은 인터페이스다. 이러한 인터페이스 뒤에는 인터페이스를 조작하는 모델(데이터 구조와 함수로 구성된 정교한 집합)이 존재한다. 그리고 모델은 인터페이스를 전혀 필요로 하지 않는다. 인터페이스는 모델에게 있어 중요하지 않다. 중요한 것은 업무 규칙이다.

따라서 이번에도 GUI와 BusinessRule 컴포넌트가 경계선에 의해 분할된다(그림17.4). 관련성이 낮은 컴포넌트가 관련성이 높은 컴포넌트에 의존한다.

![GUI와 BusinessRule 컴포넌트 사이의 경계](/images/2019/11/05/17_4.png "GUI와 BusinessRule 컴포넌트 사이의 경계"){: .center-image }

GUI는 다른 종류의 인터페이스로 얼마든지 교체할 수 있으며 BusinessRule는 전혀 개의치 않는다는 사실을 알 수 있다.

### 플러그인 아키텍처
소프트웨어 개발 기술의 역사는 플러그인을 손쉽게 생성하여, 확장 가능하며 유지보수가 쉬운 시스템 아키텍처를 확립할 수 있게 만드는 방법에 대한 이야기다. 선택적이거나 또는 수많은 다양한 형태로 구현될 수 있는 나머지 컴포넌트로부터 핵심적인 업무 규칙은 분리되어 있고, 또한 독립적이다(그림 17.5)

![업무 규칙에 플러그인 형태로 연결하기](/images/2019/11/05/17_5.png "업무 규칙에 플러그인 형태로 연결하기"){: .center-image }

### 플러그인에 대한 논의
예를 들어 누군가가 웹 페이지의 포맷을 변경하거나 데이터베이스 스키마를 변경하더라도 업무 규칙은 깨지지 않기를 바란다. 마찬가지로 시스템에서 한 부분이 변경되더라도 관련 없는 나머지 부분이 망가지길 원치 않는다.

시스템을 플러그인 아키텍처로 배치함으로써 변경이 전파될 수 없는 방화벽을 생성할 수 있다. GUI가 업무 규칙에 플러그인 형태로 연결되면 GUI에서 발생한 변경은 절대로 업무 규칙에 영향을 미칠 수 없다.

GUI는 업무 규칙과는 다른 시점에 다른 속도로 변경되므로, 둘 사이에는 반드시 경계가 필요하다. 업무 규칙은 의존성 주입 프레임워크와는 다른 시점에 그리고 다른 이유로 변경되므로, 둘 사이에도 반드시 경계가 필요하다.

---

# 18장. 경계 해부학

### 경계 횡단하기
런타임에 경계를 횡단한다. 함은 그저 경계 한쪽에 있는 기능에서 반대편 기능을 호출하여 데이터를 전달하는 일에 불과하다. 적절한 위치에서 경계를 횡단하게 하는 비결은 소스 코드 의존성 관리에 있다.

### 두려운 단일체
가장 단순한 형태의 경계 횡단은 저수준 클라이언트에서 고수준 서비스로 향하는 함수 호출이다. 이 경우 런타임 의존성과 컴파일타임 의존성은 모두 같은 방향, 즉 저수준 컴포넌트에서 고수준 컴포넌트로 향한다.

고수준 클라이언트가 저수준 서비스를 호출해야 한다면 동적 다형성을 사용하여 제어흐름과는 반대 방향으로 의존성을 역전시킬 수 있다. 이렇게 하면 런타임 의존성은 컴파일타임 의존성과는 반대가 된다. 그림18.2에서 주목할 점은 경계를 횡단할 때 의존성은 모두 오른쪽에서 왼쪽으로, 즉 **고수준 컴포넌트를 향한다** 는 점이다. 또한 데이터 구조의 정의가 호출하는 쪽에 위치한다는 점도 주목하자.

![제어흐름과는 반대로 경계를 횡단한다.](/images/2019/11/05/18_2.png "제어흐름과는 반대로 경계를 횡단한다."){: .center-image }

정적 링크된 모노리티 구조의 실행 파일이라도 이처럼 규칙적인 방식으로 구조를 분리하면 프로젝트를 개발, 테스트, 배포하는 작업에 큰 도움이 된다.

### 배포형 컴포넌트
.NET DLL, 자바 jar 파일, 루비 젬 Gem, 유닉스 공유 라이브러리 등의 동적 링크 라이브러리들은 아키텍처의 경계가 물리적으로 드러난다. 컴포넌트를 이 형태로 배포하면 따로 컴파일하지 않고 곧바로 사용할 수 있다. 배포 과정에서만 차이가 날 뿐, 단일체와 동일하다.

### 스레드
스레드는 아키텍처 경계도 아니며 배포 단위도 아니다. 스레드는 실행 계획과 순서를 체계화하는 방법에 가깝다.

### 로컬 프로세스
로컬 프로세스 간 분리 전략은 단일체나 바이너리 컴포넌트의 경우와 동일하다. 소스 코드 의존성의 화살표는 단일체나 바이너리 컴포넌트와 동일한 방향으로 경계를 횡단한다. 즉, 항상 고수준 컴포넌트를 향한다.

### 서비스
물리적인 형태를 띠는 가장 강력한 경계는 바로 서비스다. 서비스는 자신의 물리적 위치에 구애 받지 않고, 모든 통신이 네트워크를 통해 이뤄진다고 가정한다.

저수준 서비스는 반드시 고수준 서비스에 \'플러그인\' 되어야 한다. 고수준 서비스의 소스 코드에는 저수준 서비스를 특정 짓는 어떤 물리적인 정보(예를 들면, URI)도 절대 포함해서는 안 된다.

---

# 19장. 정책과 수준
좋은 아키텍처라면 각 컴포넌트를 연결할 때 의존성의 방향이 컴포넌트의 수준을 기반으로 연결되도록 만들어야 한다. 즉, 저수준 컴포넌트가 고수준 컴포넌트에 의존하도록 설계되어야 한다.

### 수준
시스템의 입력과 출력 모두로부터 멀리 위치할수록 정책의 수준은 높아진다. 입력과 출력을 다루는 정책이라면 시스템에서 최하위 수준에 위치한다.

![간단한 암호화 프로그램](/images/2019/11/05/19_1.png "간단한 암호화 프로그램"){: .center-image }

번역 컴포넌트는 이 시스템에서 최고 수준의 컴포넌트인데, 입력과 출력으로부터 가장 멀리 떨어져 있기 때문이다. 데이터 흐름과 소스 코드 의존성이 항상 같은 방향을 가리키지는 않는다.

```java
// 잘못된 아키텍처.
function encrypt() {
  while (true)
    writeChar(translate(readChar()));
}
```

위 코드는 고수준인 encrypt 함수가 저수준인 readChar와 writeChar 함수에 의존하기 때문에 잘못된 아키텍처이다.

![시스템의 더 나은 아키텍처를 보여주는 클래스 다이어그램](/images/2019/11/05/19_1.png "시스템의 더 나은 아키텍처를 보여주는 클래스 다이어그램"){: .center-image }

이 구조에서 고수준의 암호화 정책을 저수준의 입력/출력 정책으로부터 분리시킨 방식에 주목하자. 이 방식 덕분에 이 암호화 정책을 더 넓은 맥락에서 사용할 수 있다. 입력과 출력에 변화가 생기더라도 암호화 정책은 거의 영향을 받지 않기 때문이다.

정책을 컴포넌트로 묶는 기준은 정책이 변경되는 방식에 달려있다는 사실을 상기하자. 단일 책임 원칙 *SRP* 과 공통 폐쇄 원칙 *CCP* 에 따르면 동일한 이유로 동일한시점에 변경되는 정책은 항상 묶인다. 고수준 정책, 즉 입력과 출력에서부터 멀리 떨어진 정책은 저수준 정책에 비해 덜 빈번하게 변경되고, 보다 중요한 이유로 변경되는 경향이 있다.

---

# 20장. 업무 규칙

### 엔티티
엔티티는 핵심 업무 데이터를 기반으로 동작하는 일련의 조그만 핵심 업무 규칙을 구체화한다. 엔티티의 인터페이스는 핵심 업무 데이터를 기반으로 동작하는 핵심 업무 규칙을 구현한 함수들로 구성된다.

이러한 종류의 클래스를 생성할 때, 업무에서 핵심적인 개념을 구현하는 소프트웨어는 한데 모으고, 구축 중인 자동화 시스템의 나머지 모든 고려사항과 분리시킨다.

### 유스케이스
유스케이스는 시스템이 사용자에게 어떻게 보이는지를 설명하지 않는다. 이보다는 애플리케이션에 특화된 규칙을 설명하며, 이를 통해 사용자와 엔티티 사이의 상호작용을 규정한다.

엔티티는 자신을 제어하는 유스케이스에 대해 아무것도 알지 못한다. 엔티티와 같은 고수준 개념은 유스케이스와 같은 저수준 개념에 대해 아무것도 알지 못한다. 왜냐하면 유스케이스는 단일 애플리케이션에 특화되어 있으며, 따라서 해당 시스템이 입력과 출력에 보다 가깝게 위치하기 때문이다. 엔티티는 수많은 다양한 애플리케이션에서 사용될 수 있도록 일반화된 것이므로, 각 시스템의 입력이나 출력에서 더 멀리 떨어져 있다.

### 요청 및 응답 모델
유스케이스는 단순한 요청 데이터 구조를 입력으로 받아들이고, 단순한 응답 데이터 구조를 출력으로 반환한다. 이들 데이터 구조는 어떤 것에도 의존하지 않는다.

시간이 지나면 엔티티와 요청/응답 모델은 완전히 다른 이유로 변경될 것이고, 따라서 어떤 식으로든 함께 묶는 행위는 공통 폐쇄 원칙과 단일 책임 원칙을 위배하게 된다.

### 결론
- 업무 규칙은 소프트웨어 시스템이 존재하는 이유다.
- 업무 규칙은 핵심적인 기능이다.
- 업무 규칙은 사용자 인터페이스나 데이터베이스와 같은 저수준의 관심사로 인해 오염되어서는 안 되며, 원래 그대로의 모습으로 남아 있어야 한다.

---

# 21장. 소리치는 아키텍처

### 아키텍처의 목적
좋은 아키텍처는 유스케이스를 그 중심에 두기 때문에, 프레임워크나 도구, 환경에 전혀 구애받지 않고 유스케이스를 지원하는 구조를 아무런 문제 없이 기술할 수 있다. 주택에 대한 계획서를 다시 한번 생각해 보자. 아키텍트가 주목하는 첫 번째 관심사는 주택이 거주하기에 적합한 공간임을 확실히 하는 것이지, 벽돌로 지어지는지를 확인하는 것이 아니다.

### 하지만 웹은?
애플리케이션이 웹을 통해 전달된다는 사실은 세부사항이며, 시스템 구조를 지배해서는 절대 안 된다. 실제 애플리케이션을 웹으로 전달할지 여부는 미루어야 할 결정사항 중 하나다.

### 테스트하기 쉬운 아키텍처
아키텍처가 유스케이스를 최우선으로 한다면, 그리고 프레임워크와는 적당한 거리를 둔다면, 프레임워크를 전혀 준비하지 않더라도 필요한 유스케이스 전부에 대해 단위 테스트를 할 수 있어야 한다.

엔티티 객체는 반드시 오래된 방식의 간단한 객체 *plain old object* 여야 하며, 프레임워크나 데이터베이스, 또는 여타 복잡한 것들에 의존해서는 안 된다.

최종적으로, 프레임워크로 인한 어려움을 겪지 않고도 반드시 이 모두를 있는 그대로 테스트할 수 있어야 한다.

---

# 22장. 클린 아키텍처
아키텍처는 최소한 업무 규칙을 위한 계층 하나와, 사용자와 시스템 인터페이스를 위한 또 다른 계층 하나를 반드시 포함한다.

- **프레임워크 독립성**. 아키텍처는 다양한 기능의 라이브러리를 제공하는 소프트웨어, 즉 프레임워크의 존재 여부에 의존하지 않는다.
- **테스트 용이성**. 업무 규칙은 UI, 데이터베이스, 웹 서버, 또는 여타 외부 요소가 없이도 테스트할 수 있다.
- **UI 독립성**. 시스템의 나머지 부분을 변경하지 않고도 UI를 쉽게 변경할 수 잇다.
- **데이터베이스 독립성**. 업무 규칙은 데이터베이스에 결합되지 않는다.
- **모든 외부 에이전시에 대한 독립성**. 실제로 업무 규칙은 외부 세계와의 인터페이스에 대해 전혀 알지 못한다.

![클린 아키텍처](/images/2019/11/05/22_1.png "클린 아키텍처"){: .center-image }

### 의존성 규칙
바깥쪽 원은 메커니즘이고, 안쪽 원은 정책이다. 이러한 아키텍처가 동작하도록 하는 가장 중요한 규칙은 **의존성 규칙** *Dependency rule* 이다.

> 소스 코드 의존성은 반드시 안쪽으로, 고수준의 정책을 향해야 한다.

내부의 원에 속한 요소는 외부의 원에 속한 어떤 것도 알지 못한다. 특히 내부의 원에 속한 코드느 외부의 원에 선언된 어떤 것에 대해서도 그 이름을 언급해서는 절대 안 된다.

같은 이유로, 외부의 원에 선언된 데이터 형식도 내부의 원에서 절대로 사용해서는 안 된다. 특히 그 데이터 형식이 외부의 원에 있는 프레임워크가 생성한 것이라면 더더욱 사용해서는 안 된다.

**엔티티**<br/>
엔티티는 전사적인 핵심 업무 규칙을 캡슐화한다. 메서드를 가지는 객체이거나 일련의 데이터 구조와 함수의 집합일 수도 있다. 운영 관점에서 특정 애플리케이션에 무언가 변경이 필요하더라도 엔티티 계층에는 절대로 영향을 주어서는 안 된다.

**유스케이스**<br/>
유스케이스 계층의 소프트웨어는 **애플리케이션에 특화된 업무 규칙** 을 포함한다. 또한 시스템의 모든 유스케이스를 캡슐화하고 구현한다. 유스케이스는 엔티티로 들어오고 나가는 데이터 흐름을 조정하며, 엔티티가 자신의 핵심 업무 규칙을 사용해서 유스케이스의 목적을 달성하도록 이끈다. 운영 관점에서 애플리케이션이 변경된다면 유스케이스가 영향을 받는다.

**인터페이스 어댑터**<br/>
이 계층은 데이터를 엔티티와 유스케이스에게 가장 편리한 형식에서 영속성용으로 사용 중인 임의의 프레임워크가 이용하기에 가장 편리한 형식으로 반환한다.

**프레임워크와 드라이버**<br/>
프레임워크와 드라이버 계층은 모든 세부사항이 위치하는 곳이다. 웹은 세부사항이다. 데이터베이스는 세부사항이다. 이러한 것들을 모두 외부에 위치시켜서 피해를 최소화한다.

**경계 횡단하기**<br/>
예를 들어 유스케이스에서 프레젠터를 호출해야 한다고 가정해 보자. 이때 직접 호출하면 **의존성 규칙**(내부의 원에서는 외부 원에 있는 어떤 이름도 언급해서는 안 된다)을 위배한다. 따라서 유스케이스가 내부 원의 인터페이스를 호출하도록 하고, 외부 원의 프레젠터가 그 인터페이스를 구현하도록 만든다.

**경계를 횡단하는 데이터는 어떤 모습인가?**<br/>
경계를 가로질러 데이터를 전달할 때, 데이터는 항상 내부의 원에서 사용하기에 가장 편리한 형태를 가져야만 한다.

---

# 23장. 프레젠터와 험블 객체

### 험블 객체 패턴
**험블 객체** 패턴은 디자인 패턴으로, 테스트하기 어려운 행위와 테스트하기 쉬운 행위를 단위 테스트 작성자가 분리하기 쉽게 하는 방법으로 고안되었다. 행위들을 두 개의 모듈 또는 클래스로 나눈다. 이들 모듈 중 하나가 험블 *humble* 이다. 가장 기본적인 본질은 남기고, 테스트하기 어려운 행위를 모두 험블 객체로 옮긴다. 나머지 모듈에는 험블 객체에 속하지 않은, 테스트하기 쉬운 행위를 모두 옮긴다.

### 프레젠터와 뷰
뷰는 험블 객체이고 테스트하기 어렵다. 이 객체에 포함된 코드는 가능한 한 간단하게 유지한다. 뷰는 데이터를 GUI로 이동시키지만, 데이터를 직접 처리하지는 않는다.

프레젠터는 테스트하기 쉬운 객체다. 프레젠터의 역할은 애플리케이션으로부터 데이터를 받아 화면에 표현할 수 있는 포맷으로 만드는 것이다. 이를 통해 뷰는 데이터를 화면으로 전달하는 간단한 일만 처리하도록 만든다.

뷰는 뷰 모델의 데이터를 화면으로 로드할 뿐이며, 이 외에 뷰가 맡은 역할은 전혀 없다. 따라서 뷰는 보잘것없다 *humble*.

### 테스트와 아키텍처
테스트 용이성은 좋은 아키텍처가 지녀야 할 속성이다. **험블 객체** 패턴이 좋은 예인데, 행위를 테스트하기 쉬운 부분과 어려운 부분으로 분리하면 아키텍처 경계가 정의되기 때문이다.

### 데이터베이스 게이트웨이
유스케이스 계층은 SQL을 허용하지 않는다. 따라서 유스케이스 계층은 필요한 메서드를 제공하는 게이트웨이 인터페이스를 호출한다. 그리고 인터페이스의 구현체는 데이터베이스 계층에 위치한다. 이 구현체는 험블 객체다. 구현체에서 직접 SQL을 사용하거나 데이터베이스에 대한 임의의 인터페이스를 통해 게이트웨이의 메서드에서 필요한 데이터에 접근한다.

### 결론
경계를 넘나드는 통신은 거의 모두 간단한 데이터 구조를 수반할 때가 많고, 대개 그 경계는 테스트하기 어려운 무언가와 테스트하기 쉬운 무언가로 분리될 것이다. 그리고 이러한 아키텍처의 경계에서 험블 객체 패턴을 사용하면 시스템의 테스트 용이성을 크게 높일 수 있다.

---

# 24장. 부분적 경계

### 마지막 단계를 건너뛰기
부분적 경계를 생성하는 방법 하나는 독립적으로 컴파일하고 배포할 수 있는 컴포넌트를 만들기 위한 작업은 모두 수행한 후, 단일 컴포넌트에 그대로 모아만 두는 것이다. 쌍방향 인터페이스도 그 컴포넌트에 있고, 입출력 데이터 구조도 거기에 있으며, 모든 것이 완전히 준비되어 있다. 하지만 이 모두를 단일 컴포넌트로 컴파일해서 배포한다.

### 일차원 경계
다음은 추후 완벽한 형태의 경계로 확장할 수 있는 공간을 확보하고자 할 때 활용할 수 있는 더 간단한 구조다.

![전략(strategy) 패턴](/images/2019/11/05/24_1.png "전략 strategy 패턴"){: .center-image }

Client를 ServiceImpl로부터 격리시키는 데 필요한 의존성 역전이 이미 적용되었기 때문이다. 또한 이 다이어그램의 위험천만한 점선 화살표에서 보듯이 이러한 분리는 매우 빠르게 붕괴될 수 있다.

### 퍼사드
이보다 훨씬 더 단순한 경계는 의존성 역전까지도 희생한 퍼사드 *Facade* 패턴이다. Facade 클래스에는 모든 서비스 클래스를 메서드 형태로 정의하고, 서비스 호출이 발생하면 해당 서비스 클래스로 호출을 전달한다. 클라이언트는 이들 서비스 클래스에 직접 접근할 수 없다.

![퍼사드(Facade) 패턴](/images/2019/11/05/24_2.png "퍼사드 Facade 패턴"){: .center-image }

---

# 25장. 계층과 경계
UI에서 언어가 유일한 변경의 축은 아니다. 변경의 축에 의해 정의되는 아키텍처 경계가 잠재되어 있을 수 있다.

![개선된 다이어그램](/images/2019/11/05/25_3.png "개선된 다이어그램"){: .center-image }

GameRules는 GameRules가 정의하고 Language가 구현하는 API를 이용해 Language와 통신한다. 마찬가지로 Language는 Language가 정의하고 TextDelivery가 구현하는 API를 이용해 TextDelivery와 통신한다. API는 (구현하는 쪽이 아닌) 사용하는 쪽에 정의되고 소속된다.

English, SMS, CloudData와 같은 변형들은 추상 API 컴포넌트가 정의하는 다형적 인터페이스를 통해 제공되고, 실제로 서비스하는 구체 컴포넌트가 해당 인터페이스를 구현한다.

![단순화된 다이어그램](/images/2019/11/05/25_4.png "단순화된 다이어그램"){: .center-image }

위 다이어그램은 모든 화살표가 위를 향하도록 맞춰졌다. 그 결과 GameRules는 최상위 수준의 정책을 가지는 컴포넌트이므로 최상위에 놓인다. 모든 입력은 사용자로부터 전달받아 좌측 하단의 TextDelivery 컴포넌트로 전달된다. 이 정보는 Language 컴포넌트를 거쳐서 위로 올라가며, GameRules에 적합한 명령어로 번역된다. GameRules는 사용자 입력을 처리하고, 우측 하단의 DataStorage로 적절한 데이터를 내려 보낸다.

---

# 26장. 메인 컴포넌트

### 궁극적인 세부사항
메인 컴포넌트는 시스템의 초기 진입점인 가장 낮은 수준의 정책이다. 모든 팩토리 *Factory* 와 전략 *Strategy* , 그리고 시스템 전반을 담당하는 나머지 기반 설비를 생성한 후, 시스템에서 더 높은 수준을 담당하는 부분으로 제어권을 넘기는 역할을 맡는다.

의존성 주입 프레임워크를 이용해 의존성을 주입하는 일은 바로 이 메인 컴포넌트에서 이뤄져야 한다.

### 결론
메인을 애플리케이션의 플러그인이라고 생각하자. 초기 조건과 설정을 구성하고, 외부 자원을 모두 수집한 후, 제어권을 애플리케이션의 고수준 정책으로 넘기는 플러그인이다.

---

# 27장. 크고 작은 모든 서비스들

### 서비스 아키텍처?
시스템의 아키텍처는 의존성 규칙을 준수하며 고수준의 정책을 저수준의 세부사항으로부터 분리하는 경계에 의해 정의된다. 단순히 애플리케이션의 행위를 분리할 뿐인 서비스라면 값비싼 함수 호출에 불과하며, 아키텍처 관점에서 꼭 중요하다고 볼 수는 없다.

### 서비스의 이점?
**결합 분리의 오류**<br/>
물론 서비스는 개별 변수 수준에서는 각각 결합이 분리된다. 하지만 프로세서 내의 또는 네트워크 상의 공유 자원 때문에 결합될 가능성이 여전히 존재한다. 더욱이 서로 공유하는 데이터에 의해 이들 서비스는 강력하게 결합되어 버린다.

**개발 및 배포 독립성의 오류**<br/>
1. 대규모 엔터프라이즈 시스템은 서비스 기반 시스템 이외에도, 모노리틱 시스템이나 컴포넌트 기반 시스템으로도 구축할 수 있다는 사실은 역사적으로 증명되어 왔다. 따라서 서비스는 확장 가능한 시스템을 구축하는 유일한 선택지가 아니다.
2. \'결합 분리의 오류\'에 따르면 서비스라고 해서 항상 독립적으로 개발하고, 배포하며, 운영할 수 있는 것은 아니다. 데이터나 행위에서 어느 정도 결합되어 있다면 결합된 정도에 맞게 개발, 배포, 운영을 조정해야만 한다.

### 야옹이 문제
확장 가능한 시스템을 구축하고 싶었기에, 수많은 작은 마이크로 서비스를 기반으로 택시 통합 서비스를 구착하기로 결정했다. 개발팀 직원을 많은 소규모 팀으로 세분화했고, 각 팀이 팀 규모에 맞게 적당한 수의 서비스를 개발하고, 유지보수하며, 운영하는 책임을 지도록 했다.

![택시 통합 서비스를 구현하기 위해 배치된 서비스들](/images/2019/11/05/27_1.png "택시 통합 서비스를 구현하기 위해 배치된 서비스들"){: .center-image }

여기에 야옹이를 배달하는 기능을 제공해야 한다면, 이들 서비스 중 어디를 변경해야 할까? 전부다. 다시 말해 이 서비스들은 모두 결합되어 있어서 독립적으로 개발하고, 배포하거나, 유지될 수 없다. 이게 바로 횡단 관심사 *cross-cutting concern* 가 지닌 문제다. 모든 소프트웨어 시스템은 서비스 지향이든 아니든 이 문제에 직면하게 마련이다.

### 객체가 구출하다
컴포넌트 기반 아키텍처에서는 다형적으로 확장할 수 있는 클래스 집합을 생성해 새로운 기능을 처리하도록 한다. 경계와 의존성 규칙을 준수한다.

![객체 지향 방식으로 횡단 관심사를 처리하기](/images/2019/11/05/27_2.png "객체 지향 방식으로 횡단 관심사를 처리하기"){: .center-image }

배차에 특화된 로직 부분은 Rides 컴포넌트로 추출되고, 야옹이에 대한 신규 기능은 Kittens 컴포넌트에 들어갔다. 이 두 컴포넌트는 기존 컴포넌트들에 있는 추상 기반 클래스를 **템플릿 메서드** *Template method* 나 **전략 패턴** *Strategy* 등을 이용해서 오버라이드한다. 야옹이 기능은 결합이 분리되며, 독립적으로 개발하여 배포할 수 있다.

### 컴포넌트 기반 서비스
서비스가 반드시 소규모 단일체 *monolith* 여야 할 이유는 없다. 서비스는 SOLID 원칙대로 설계할 수 있으며 컴포넌트 구조를 갖출 수도 있다. 이를 통해 서비스 내의 기존 컴포넌트들을 변경하기 않고도 새로운 컴포넌트를 추가할 수 있다.

![각 서비스의 내부는 각자의 방식대로 컴포넌트를 설계할 수 있으며, 파생 클래스를 만들어서 신규 기능을 추가할 수 있다.](/images/2019/11/05/27_3.png "각 서비스의 내부는 각자의 방식대로 컴포넌트를 설계할 수 있으며, 파생 클래스를 만들어서 신규 기능을 추가할 수 있다."){: .center-image }

위 그림의 서비스 다이어그램에서 서비스들의 존재는 이전과 달라진게 없지만, 각 서비스의 내부는 자신만의 컴포넌트 설계로 되어 있어서 파생 클래스를 만드는 방식으로 신규 기능을 추가할 수 있다. 파생 클래스들은 각자의 컴포넌트 내부에 놓인다.

### 횡단 관심사
아키텍처 경계가 서비스 사이에 있지 않고, 서비스를 관통하며 서비스를 컴포넌트 단위로 분할한다.

모든 주요 시스템이 직면하는 횡단 관심사를 처리하려면, 아래 다이어그램처럼 서비스 내부의 **의존성 규칙** 도 준수하는 컴포넌트 아키텍처로 설계해야 한다. 이 서비스들은 시스템의 아키텍처 경계를 정의하지 않는다. 아키텍처 경계를 정의하는 것은 서비스 내에 위치한 컴포넌트다.

![서비스 내부는 의존성 규칙도 준수하는 컴포넌트 아키텍처로 설계해야 한다.](/images/2019/11/05/27_4.png "서비스 내부는 의존성 규칙도 준수하는 컴포넌트 아키텍처로 설계해야 한다."){: .center-image }

### 결론
서비스는 시스템의 확장성과 개발 가능성 측면에서는 유용하지만, 그 자체로는 아키텍처적으로 그리 중요한 요소는 아니다. 시스템의 아키텍처는 시스템 내부에 그어진 경계를 넘나드는 의존성에 의해 정의된다.

---

# 28장. 테스트 경계

### 시스템 컴포넌트인 테스트
- 테스트는 태생적으로 **의존성 규칙** 을 따른다. 테스트는 세부적이며 구체적인 것으로, 의존성은 항상 테스트 대상이 되는 코드를 향한다. 실제로 테스트는 아키텍처에서 항상 테스트 대상이 되는 코드를 향한다. 실제로 테스트는 아키텍처에서 가장 바깥쪽 원으로 생각할 수 있다.
- 테스트는 독립적으로 배포 가능하다.
- 테스트는 시스템 컴포넌트 중에서 가장 고립되어 있다. 테스트가 시스템 운영에 꼭 필요치는 않다. 어떤 사용자도 테스트에 의존하지 않는다.

### 테스트를 고려한 설계
테스트가 시슽메의 설계와 잘 통합되지 않으면, 테스트는 깨지기 쉬워지고, 시스템은 뻣뻣해져서 변경하기가 어려워진다.

시스템에 강하게 결합된 테스트라면 시스템이 변경될 때 함께 변경되어야만 한다. 시스템 컴포넌트에서 생긴 아주 사소한 변경도, 이와 결합된 수많은 테스트를 망가뜨릴 수 있다.

이 문제를 해결하려면 테스트를 고려해서 설계를 해야 한다. **변동성 있는 것에 의존하지 말라.**

### 테스트 API
이 목표를 달성하려면 테스트가 모든 업무 규칙을 검증하는 데 사용할 수 있도록 특화된 API를 만들면 된다. 이 API는 사용자 인터페이스가 사용하는 **인터랙터** *Interactor* 와 **인터페이스 어댑터** *Interface Adapter* 들의 상위 집합이 될 것이다.

테스트 API는 테스트를 애플리케이션으로부터 분리할 목적으로 사용한다.

**구조적 결합**<br/>
모든 상용 클래스에 테스트 클래스가 각각 존재하고, 또 모든 상용 메서드에 테스트 메서드 집합이 각각 존재하는 테스트 스위트가 있다고 가정해 보자.

상용 클래스나 메서드 중 하나라도 변경되면 딸려 있는 다수의 테스트가 변경되어야 한다. 결과적으로 테스트는 깨지기 쉬워지고, 이로 인해 상용 코드를 뻣뻣하게 만든다.

테스트 API의 역할은 애플리케이션의 구조를 테스트로부터 숨기는 데 있다. 이렇게 만들면 상용 코드를 리팩터링하거나 진화시키더라도 테스트에는 전혀 영향을 주지 않는다. 또한 테스트를 리팩터링하거나 진화시킬 때도 상용 코드에는 전혀 영향을 주지 않는다.

**보안**<br/>
테스트 API 자체와 테스트 API 중 위험한 부분의 구현부는 독립적으로 배포할 수 있는 컴포넌트로 분리해야 한다.

---

# 29장. 클린 임베디드 아키텍처

> 소프트웨어는 닳지 않지만, 펌웨어와 하드웨어에 대한 의존성을 관리하지 않으면 안으로부터 파괴될 수 있다.

펌웨어를 수없이 양산하는 일을 멈추고, 코드에게 유효 수명을 길게 늘릴 수 있는 기회를 주어라.

## 앱-티튜드 테스트
켄트 벡 *Kent Beck* 은 소프트웨어를 구축하는 세 가지 활동을 다음과 같이 기술했다.

- 먼저 동작하게 만들어라.
- 그리고 올바르게 만들어라.
- 그리고 빠르게 만들어라.

앱이 동작하도록 만드는 것을 나는 개발자용 **앱-티튜드 테스트** *App-titude test* 라고 부른다. 프로그래밍에는 단순히 앱이 동작하도록 만드는 것보다 중요한 것이 훨씬 많다.

### 타킷-하드웨어 병목현상
임베디드 코드가 클린 아키텍처 원칙과 실천법을 따르지 않고 작성된다면, 대개의 경우 코드를 테스트할 수 있는 환경이 해당 특정 타깃으로 국한될 것이다. 그리고 그 타깃이 테스트가 가능한 유일한 장소라면 **타깃-하드웨어 병목현상** *target-hardware bottleneck* 이 발생하여 진척이 느려질 것이다.

**클린 임베디드 아키텍처는 테스트하기 쉬운 임베디드 아키텍처다.**<br/>
임베디드 소프트웨어 개발자가 해야 할 일 하나는 이 경계를 분명하게 만드는 것이다. 소프트웨어와 펌웨어 사이의 경계는 하드웨어 추상화 계층 *Hardware Abstraction Layer, HAL* 이라고 부른다.

![하드웨어 추상화 계층](/images/2019/11/05/29_4.png "하드웨어 추상화 계층"){: .center-image }

HAL은 자신보다 위에 있는 소프트웨어를 위해 존재하므로, HAL의 API는 소프트웨어의 필요에 맞게 만들어져야 한다.

**HAL 사용자에게 하드웨어 세부사항을 드러내지 말자**<br/>
클린 임베디드 아키텍처로 설계된 소프트웨어는 타깃 하드웨어에 관계없이 테스트가 가능하다. 프로세서와 운영체제는 세부사항이다. 마찬가지로 클린 임베디드 아키텍처로 설계된 소프트웨어는 타깃 프로세서와 운영체제에 관계없이 테스트할 수 있다. 각 타깃과는 별개로 테스트할 수 있도록 해주는 경계층 또는 일련의 대체 지점을 제공한다.

**인터페이스를 통하고 대체 가능성을 높이는 방향으로 프로그래밍하라**<br/>
계층형 아키텍처 *layered architecture* 는 인터페이스를 통해 프로그래밍하자는 발상을 기반으로 한다. 모듈들이 서로 인터페이스를 통해 상호작용한다면 특정 서비스 제공자를 다른 제공자로 대체할 수 있다.

오직 구현체에서만 필요한 데이터 구조, 상수, 타입 정의들로 인터페이스 헤더 파일을 어지럽히지 말라. 세부사항을 알고 있는 부분이 적을수록 추적하고 변경해야 할 코드도 적어진다.

클린 임베디드 아키텍처에서는 모듈들이 인터페이스를 통해 상호작용하기 때문에 각각의 계층 내부에서 테스트가 가능하다. 각 인터페이스는 타깃과는 별개로 테스트할 수 있도록 해주는 경계층 또는 대체 지점을 제공한다.

---

# 30장. 데이터베이스는 세부사항이다
아키텍처 관점에서 데이터베이스는 엔티티가 아니다. 세부사항이라서 아키텍처의 구성요소 수준으로 끌어올릴 수 없다. 데이터베이스는 데이터에 접근할 방법을 제공하는 유틸리티다. 아키텍처 관점에서 보면 이러한 유틸리는 저수준의 세부사항일 뿐이라서 아키텍처와는 관련이 없다.

### 관계형 데이터베이스
데이터를 테이블에 행 단위로 배치한다는 자체는 아키텍처적으로 볼 때 전혀 중요하지 않다. 데이터가 테이블 구조를 가진다는 사실은 오직 아키텍처의 외부 원에 위치한 최하위 수준의 유틸리티 함수만 알아야 한다.

### 데이터베이스 시스템은 왜 이렇게 널리 사용되는가?
디스크 때문에 피해갈 수 없는 시간 지연이라는 짐을 완화하기 위해 색인, 캐시, 쿼리 최적화가 필요해졌다. 그리고 데이터를 표현하는 표준적인 방식도 필요해졌다. 시간이 지나면서 이러한 시스템은 두 가지 유형을 분리되었는데, 하나는 파일 시스템이었고 다른 하나는 관계형 데이터베이스 관리 시스템 *RDBMS* 이었다.

이들 두 시스템은 데이터를 디스크에 최적화해서, 각 시스템에 특화된 방식으로 접근해야 할 때 가능한 효율적으로 데이터를 저장하고 검색할 수 있도록 한다.

### 결론
체계화된 데이터 구조와 데이터 모델은 아키텍처적으로 중요하다. 반면, 그저 데이터를 회전식 자기 디스크 표면에서 이리저리 옮기는 기술과 시스템은 아키텍처적으로 중요치 않다. 데이터를 테이블 구조로 만들고 SQL로만 접근하도록 하는 관계형 데이터베이스 시스템은 전자보다는 후자와 훨씬 관련이 깊다. 데이터는 중요하다. 데이터베이스는 세부사항이다.

---

# 31장. 웹은 세부사항이다
GUI인 웹은 세부사항이다. 세부사항을 핵심 업무 로직에서 분리된 경계 바깥에 두어야 한다.

완전한 입력 데이터와 그에 따른 출력 데이터는 데이터 구조로 만들어서 유스케이스를 실행하는 처리 과정의 입력 값과 출력 값으로 사용할 수 있다. 이 방식을 따르면 각 유스케이스가 장치 독립적인 방식으로 UI라는 입출력 장치를 동작시킨다고 간주할 수 있다.

---

# 32장. 프레임워크는 세부사항이다

### 프레임워크 제작자
프레임워크 제작자는 자신이 해결해야 할 고유한 문제나 자신의 동료와 친구들의 문제를 알고 있다. 그리고 그러한 문제들을 해결하기 위해 프레임워크를 만든다. 당신의 문제를 해결하기 위해서가 아니다.

### 위험 요인
- 프레임워크의 아키텍처는 그다지 깔끔하지 않은 경우가 많다. 프레임워크는 의존성 규칙을 위반하는 경향이 있다.
- 프레임워크는 애플리케이션의 초기 기능을 만드는 데는 도움이 될 것이다. 하지만 제품이 성숙해지면서 프레임워크가 제공하는 기능과 틀을 벗어나게 될 것이다.
- 프레임워크는 당신에게 도움되지 않는 방향으로 진화할 수도 있다.

### 해결책
업무 객체를 만들 때 프레임워크가 자신의 기반 클래스로부터 파생하기를 요구한다면, 거절하라! 대신 프락시 *proxy* 를 만들고, 업무 규칙에 플러그인할 수 있는 컴포넌트에 프락시를 위치시켜라.

---

# 33장. 사례 연구: 비디오 판매

### 유스케이스 분석
단일 책임 원칙에 따르면 이들 네 액터가 시스템이 변경되어야 할 네 가지 주요 근원이 된다. 신규 기능을 추가하거나 기존 기능을 변경해야 한다면, 그 이유는 반드시 이들 액터 중 하나에게 해당 기능을 제공하기 위해서다.

![전형적인 유스케이스 분석](/images/2019/11/05/33_1.png "전형적인 유스케이스 분석"){: .center-image }

중앙의 점선으로 된 유스케이스를 주목하자. 이들은 추상 유스케이스다. 추상 유스케이스는 범용적인 정책을 담고 있으며, 다른 유스케이스에서 이를 더 구체화한다.

### 컴포넌트 아키텍처
뷰, 프레젠터, 인터랙터, 컨트롤러로 분리된 전형적인 분할 방법을 확인할 수 있다. 또한 대응하는 액터에 따라 카테고리를 분리했다는 사실도 확인할 수 있다.

![예비 단계의 컴포넌트 아키텍처](/images/2019/11/05/33_2.png "예비 단계의 컴포넌트 아키텍처"){: .center-image }

### 의존성 관리
제어흐름은 오른쪽에서 왼쪽으로 이동한다. 입력이 컨트롤러에서 발생하면 인터랙터에 의해 처리되어 결과가 만들어진다. 그런 후 프레젠터가 결과의 포맷을 변경하고, 뷰가 화면에 표시한다.

모든 의존성은 경계선을 한 방향으로만 가로지르는데, 항상 더 높은 수준의 정책을 포함하는 컴포넌트를 향한다.

---

# Reference
- [클린 아키텍처: 소프트웨어 구조와 설계의 원칙](http://www.kyobobook.co.kr/product/detailViewKor.laf?barcode=9788966262472)
- [Clean Architecture](http://putregai.com/sbooks/clean_arch.pdf)
