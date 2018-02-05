---
layout: post
title:  "[HTTP: The Definitive Guide] 6. 프록시"
date:   2018-01-31 12:05:22 +0900
background: '/img/posts/01.jpg'
categories: http
---

## 웹 중개자
---
웹 프록시 서버는 클라이언트 입장에서 트랙잭션을 수행하는 **중개인**이다. 클라이언트는 HTTP 서버와 대화하는 대신,
자신의 입장에서 서버와 대화해주는 프록시와 대화한다. 

`트랜잭션`을 완료하는 것이 클라이언트라는 점은 변하지 않지만, 프록시 서버가 제공하는 **좋은 서비스**를 이용할 수 있다.

> HTTP 프록시 서버는 `웹 서버`이기도 하고, `웹 클라이언트`이기도 하다.

프록시는 HTTP 클라이언트의 요청을 받게 되므로, 반드시 웹 서버처럼 요청과 커넥션을 다루고 응답을 돌려줘야 한다.
 
동시에 프록시는 요청을 서버로 보내기도 하므로, 요청을 보내고 응답을 받는 올바른 HTTP 클라이언트처럼 동작해야 한다.

개인 프록시와 공용 프록시
: 프록시 서버는 하나의 클라이언트가 **독점적으로** 사용할 수도 있고, 여러 클라이언트가 **공유**할 수도 있다.

: 하나의 클라이언트만을 위한 프록시를 `개인 프록시`라고 부르고, 여러 클라이언트*가 함께 사용하는 프록시는 `공용 프록시`라고 부른다.

1. 공용 프록시
- 대부분의 프록시는 공용이며 공유된 프록시다. `중앙 집중형` 프록시를 관리하는 것이 더 효율적이고 쉽다.
- 그리고 `캐시 프록시 서버`와 같은 몇몇 프록시 애플리케이션은 프록시를 이용하는 사용자가 많을수록 유리하다.
왜냐하면 여러 사용자들의 **공통된 요청**에서 이득을 취할 수 있기 때문이다.

2. 개인 프록시
- `개인 프록시`는 흔하진 않지만 지속적으로 사용되고 있다. 특히 클라이언트 컴퓨터에서 직접 실행되는 형태로 사용된다.
- 특정 브라우저나 보조 제품들은 몇몇 
[ISP 서비스](https://ko.wikipedia.org/wiki/%EC%9D%B8%ED%84%B0%EB%84%B7_%EC%84%9C%EB%B9%84%EC%8A%A4_%EC%A0%9C%EA%B3%B5%EC%9E%90)
와 마찬가지로 **브라우저의 기능을 확장**, **성능을 개선**하거나
무료 ISP 서비스를 위한 **광고를 운영**하기 위해 프록시를 사용자의 컴퓨터에서 직접 실행한다.

프록시 vs 게이트웨이
: `프록시`는 같은 프로토콜을 사용하는 둘 이상의 애플리케이션을 연결하고, 
`게이트웨이`는 서로 다른 프로토콜을 사용하는 둘 이상을 연결한다.

: 게이트웨이는 클라이언트와 서버가 서로 다른 프로토콜로 말하더라도 서로 간의 트랜잭션을 완료할 수 있도록 해주는
`프로토콜 변환기`처럼 동작한다.

: 실질적으로 프록시와 게이트웨이의 차이점은 모호하다. 브라우저와 서버는 다른 버전의 HTTP를 구현하기에,
프록시는 때때로 약간의 프로토콜 변환을 하기도 한다.

: 그리고 상용 프록시 서버는 `SSL 보안 프로토콜`, `SOCKS 방화벽`, `FTP 접근`, `웹 기반 애플리케이션`을 지원하고자
게이트웨이 기능을 구현한다.

## 왜 프록시를 사용하는가?
---
프록시 서버는 실용적이고 유용한 것이라면 무슨 일이든 한다. `보안`을 개선하고, `성능`을 높여주며, `비용`을 절약한다.
그리고 프록시 서버는 모든 `HTTP 트래픽`을 들여다보고 건드릴 수 있기에 트래픽을 감시하고 수정할 수 있다.
다음은 프록시의 활용 예이다.

어린이 필터
: 미성년자인 사용자에게 성인 콘텐츠를 차단하기 위해 `필터링 프록시`를 사용할 수 있다.


문서 접근 제어자
: 프록시 서버는 많은 웹 서버들과 웹 리소스에 대한 단일한 `접근 제어 전략`을 구현하고 `감사 추적(audit trail)`을
하기 위해 사용될 수 있다. 이는 대기업이나 분산된 관료 조직에서 유용하다.

: 각기 다른 조직에서 관리되는 다양한 종류의 웹 서버들에 대한 접근 제어를 수시로 갱신할 필요 없이, `중앙 프록시 서버`에서
접근 제어를 설정할 수 있다.

> 고의적으로 제어 프록시를 피해가는 것을 방지하기 위해, 
웹 서버가 고정적으로 프록시 서버로부터의 요청만 받도록 설정할 수 있다.

보안 방화벽
: 네트워크 보안 엔지니어는 `보안`을 강화하기 위해 `방화벽 프록시` 서버를 사용한다. 프록시 서버는 조직 안에 들어오거나 나가는
`응용 레벨 프로토콜`의 흐름을 네트워크의 **한 지점**에서 통제한다. 

: 또한, 바이러스를 제거하는 웹이나 이메일 프록시가 사용할 수 있는 `후크(hook)`를 제공한다. 이를 통해 트래픽을 세심하게
살펴볼 수 있다.
> 요청과 응답은 방화벽과 필터링 라우터를 거친다.

웹 캐시
: 캐시 프록시는 자주 사용되는 문서의 `로컬 사본`을 관리하고, 해당 문서에 대한 요청이 오면 **빠르게** 제공하여
느리고 비싼 인터넷 커뮤니케이션을 줄인다.

대리 프록시(Surrogate)
: 어떤 프록시는 **웹 서버인 것처럼** 위장한다. 그렇기에 `대리 프록시(리버스 프록시)`는 진짜 웹 서버 요청을 받지만,
웹 서버와는 달리 요청 받은 컨텐츠의 **위치를 찾아내기 위해** 다른 서버와 커뮤니케이션을 시작한다.

: 대리 프록시는 `공용 컨텐츠`에 대한 느린 웹 서버의 성능을 개선하기 위해 사용할 수 있다.
이런식으로 사용되는 대리 프록시를 `서버 가속기`라고도 한다.

: 또한, 대리 프록시는 라우팅 기능과 결합되어 `주문형 복제 컨텐츠`의 분산 네트워크를 만들기 위해 사용되기도 한다.

컨텐츠 라우터
: 프록시 서버는 `인터넷 트래픽 조건`과 `컨텐츠 종류`에 따라 요청을 특정 웹 서버로 유도하는 `컨텐츠 라우터`로 동작할 수 있다.

: 콘텐츠 라우터는 사용자들에게 제공할 여러 서비스를 구현하는데 사용할 수 있다. 예를 들어 사용자가 **컨텐츠 제공자**에게
더 높은 성능을 위해 돈을 지불했다면, 컨텐츠 라우터는 요청을 가까운 복제 캐시로 전달할 수 있을 것이다.

: 만약 사용자가 **필터링 서비스**에 가입했다면, HTTP 요청이 `필터링 프록시`를 통과하도록 할 수 있을 것이다.

트랜스코더
: 프록시 서버는 컨텐츠를 클라이언트에게 전달하기 전에 `본문 포맷`을 수정할 수 있다.
이와 같이 데이터의 표현 방식을 자연스럽게 변환하는 것을 `트랜스코딩`이라고 부른다.
> 무손실 압축과 같이 상대적으로 단순한 데이터 인코딩 변환을 `트랜스코딩`으로,
> 보다 두드러진 매체 변경과 의미 변경을 `트랜스레이션`으로 정의하기도 한다. 

: 예를 들어 `트랜스코딩 프록시`는 크기를 줄이기 위해 `GIF 이미지`를 `JPG 이미지`로 변환할 수 있다.
마찬가지로 텍스트 파일을 압축시키거나, 특정 언어로 변환할 수 있다.

익명화 프록시(Anonymizer)
: `익명화 프록시`는 HTTP 메시지에서 신원을 식별할 수 있는 특성들(`IP 주소`, `From 헤더`, `Referer 헤더`, `쿠키`, `URI 세션 아이디`)
을 적극적으로 제거함으로써 `개인 정보 보호`와 `익명성 보장`에 기여한다.
> 그러나 클라이언트 식별 정보를 무조건적으로 제거하면 안 된다.

## 프록시는 어디에 있는가?
---
프록시 서버 배치 
: 프록시 서버는 사용 용도에 따라 어디에든 배치될 수 있다. 다음은 프록시 서버가 배치될 수 있는 방법이다.

1. 출구(Egress) 프록시
- `로컬 네트워크(LAN)`와 `인터넷` 사이를 오가는 트래픽을 제어하기 위해 프록시를 로컬 네트워크의 **출구**에 배치할 수 있다.
- 회사 밖의 해커들을 막는 방화벽을 제공하기 위해, 인터넷 트래픽의 성능을 개선하기 위해 사용할 수 있다.
또한, 부적절한 컨텐츠를 브라우징하는 것을 막기 위해 `필터링 출구 프록시`를 사용할 수 있다.

2. 접근(입구) 프록시
- 고객으로부터의 모든 요청을 **종합적**으로 처리하기 위해 프록시는 `ISP 접근 지점`에 위치하기도 한다.
-`ISP`는 사용자들의 다운로드 속도를 개선하고 인터넷 대역폭 비용을 줄이기 위해 `캐시 프록시`를 사용하여
자주 사용되는 문서의 사본을 저장한다.

3. 대리 프록시
- 대리 프록시는 네트워크의 가장 끝에 있는 **웹 서버들의 바로 앞에 위치**하여 웹 서버로 향하는 **모든 요청을 처리**하고
필요할 때만 웹 서버에게 자원을 요청할 수 있다.
- 또한, 웹 서버에 보안 기능을 추가하거나 `웹 서버 캐시`를 웹 서버 앞에 놓음으로써 성능을 개선할 수 있다.
- 대리 프록시는 일반적으로 웹 서버의 `이름`과 `IP 주소`로 스스로를 가장하기에, 모든 요청은 이 프록시로 가게 된다.

4. 네트워크 교환 프록시
- 캐시를 이용해 인터넷 교차로의 혼잡을 완화하고 트래픽 흐름을 감시하기 위해, **충분한 처리 능력을 갖춘** 프록시가
네트워크 사이의 인터넷 `피어링` 교환 지점들에 놓일 수 있다.
> `피어링(peering)`이란, ISP간 서로 네트워크를 연결하고 트래픽을 교환하는 것을 의미한다.

프록시 계층
: 프록시들은 `프록시 계층`이라고 불리는 연쇄를 구성할 수 있다. 메시지는 최종적으로 원 서버에 도착할 때까지
프록시들을 거쳐 이동한다.

: 프록시 계층에서 프록시 서버들은 **부모와 자식 관계**를 갖는다. 다음번 `인바운드 프록시`를 부모라고 부르고,
다음번 `아웃바운드 프록시`를 자식이라고 부른다. 

프록시 계층 콘텐츠 라우팅
: 프록시 계층이 반드시 `정적`이여야 하는 것은 아니다. 프록시 서버는 여러 가지 판단 근거에 의해 메시지를
**다양하고 유동적인** 프록시 서버와 원 서버들의 집합에게 보낼 수 있다. 동적 부모 선택의 예는 다음과 같다.
> `라우팅(routing)`이란, 네트워크 통신 안에서 통신 데이터를 보낼 경로를 선택하는 과정이다.

1. 부하 균형
- 자식 프록시는 **부하를 분산**하기 위해 현재 부모들의 `작업량` 수준에 근거하여 부모 프록시를 고른다.

2. 지리적 인접성에 근거한 라우팅
- 자식 프록시는 원 서버의 지역을 담당하는 부모를 선택할 수도 있다.

3. 프로토콜/타입 라우팅
- 어떤 자식 프록시는 URI에 근거하여 다른 부모나 원 서버로 라우팅 할 수 있다.

4. 유료 서비스 가입자를 위한 라우팅
- 웹 서비스 운영자가 빠른 서비스를 지원하고자 추가금을 지불했다면, 그들의 URI는 `대형 캐시`나 성능 개선을 위한
`압축 엔진`으로 라우팅 될 수 있다.

동적 부모 라우팅 로직은 제품마다 다르게 구현된다.

프락시가 트래픽을 처리하는 방법
: 클라이언트는 보통 웹 서버와 **직접** 대화하기 때문에, 우리는 먼저 **어떻게** HTTP 트래픽이 프록시로 향하는 길을
찾아내는지 설명할 필요가 있다.
 
클라이언트 트래픽이 프록시로 가도록 만드는 방법에는 다음 방법이 있다.

1. 클라이언트를 수정한다
- 브라우저를 포함한 많은 웹 클라이언트들은 수동 혹은 자동 `프록시 설정`을 지원한다.
만약 클라이언트가 프록시를 사용하도록 설정되어 있다면, 클라이언트는 `HTTP 요청`을 프록시로 보낸다.

2. 네트워크를 수정한다
- 클라이언트는 알지도 못하고 간섭도 할 수 없는 상태에서, `네트워크 인프라`를 가로채서 웹 트래픽을
프록시로 가도록 조정할 수 있다. 
- 이는 일반적으로 HTTP 트래픽을 지켜보고 가로채어 **클라이언트 모르게** 
트래픽을 프록시로 보내는 `스위칭 장치`와 `라우팅 장치`를 필요로 한다. 이것을 `인터셉트 프록시`라고 한다.
> 인터셉터 프록시를 `투명 프록시(transparent proxy)`라고도 한다.
> 하지만 투명이라는 단어가 이미 HTTP 명세에서 **행위의 의미를 변경하지 않는다**는 
> 뜻으로 사용되고 있기에 `인터셉트 프록시`라고 명명할 것을 권장한다.

3. DNS 이름공간을 수정한다
- 웹 서버 앞에 위치하는 프록시 서버인 대리 프록시는 웹 서버의 이름과 IP 주소를 자신이 직접 사용한다.
그래서 모든 요청은 서버 대신 대리 프록시로 간다.
- 이는 `DNS 이름 테이블`을 수동으로 편집하는 프록시, 서버를 계산해주는 동적 DNS 서버를 이용해 조정될 수 있다.

4. 웹 서버를 수정한다
- 몇몇 웹 서버는 `HTTP 리다이렉션 명령(응답 코드 305)`을 클라이언트에게 돌려줌으로써 클라이언트의 요청을
프록시로 `리다이렉트` 하도록 설정할 수 있다. 클라이언트는 리다이렉트를 받는 즉시 프록시와 트랜잭션을 시작한다.

## 클라이언트 프록시 설정
---
오늘날 대부분의 `브라우저`는 프록시를 사용할 수 있도록 설정할 수 있다. 다음은 프록시를 설정할 수 있는 여러 가지 방법이다.

1. 수동 설정
- 프록시를 사용하겠다고 **명시적**으로 설정한다. 단순하지만 유연하지 못하다.
- 모든 컨텐츠를 위해 단 하나의 프록시 서버만 지정할 수 있고, 장애 시의 대체 작동에 대한 지원도 없다.

2. 브라우저 기본 설정
- `브라우저 벤더`나 `배포자`는 브라우저를 소비자에게 전달하기 전에 프록시를 **미리** 설정해 놓을 수 있다.

3. 프록시 자동 설정(Proxy auto-configuration, PAC)
- `자바스크립트 프록시 자동 설정(PAC)` 파일에 대한 URI를 제공할 수 있다. 클라이언트는 프록시를 써야하는지,
만약 그렇다면 어떤 프록시 서버를 사용해야 하는지를 판단하고자 해당 파일을 실행한다.
- 매 접근 마다 적절한 프록시 서버를 계산해주는 `자바스크립트 함수`로 이루어져 있기에, `프록시 수동 설정` 보다 동적인 해결책이다.
- PAC 파일은 일반적으로 `.pac` 확장자를 가지며 MIME 타입은 `application/x-ns-proxy-autoconfig`이다.
- PAC 파일 내에 `FindProxyForUri(url, host)` 함수는 사용할 프록시 서버를 계산해주는 역할을 하며,
`반환값`은 `DIRECT`, `PROXY host:port`, `SOCKS host:port` 중 하나이다.

4. WPAD 프록시 발견
    - 대부분의 브라우저는 자동설정 파일을 다운받을 수 있는 `설정 서버`를 자동으로 찾아주는,
    `웹 프록시 자동 발견 프로토콜(Web Proxy Autodiscovery Protocol, WPAD)`을 제공한다.
    - WPAD 프로토콜이 구현된 클라이언트가 하게 될 일은 다음과 같다.
        - `PAG URI`를 찾기 위해 WPAD를 사용한다.
        - 주어진 URI에서 `PAR 파일`을 가져온다.
        - 프록시 서버를 알아내기 위해 PAC 파일을 실행한다.
        - 알아낸 프록시 서버를 이용해서 요청을 처리한다.

## 프록시 요청의 미묘한 특징들
---
프록시 URI는 서버 URI와 다르다
: 웹 서버와 웹 프록시 메시지의 문법은 서로 같지만, **한 가지 예외**가 있다. 클라이언트가 프록시 대신 서버로 요청을 보내면
요청의 URI가 달라진다.

: 클라이언트가 웹 서버로 요청을 보낼 때, `요청줄`은 다음의 예와 같이 `스킴`, `호스트`, `포트번호`가 없는 `부분 URI`를 가진다.
~~~
    GET /index.html HTTP/1.0
    User-Agent: SuperBrowserv1.3
~~~

: 그러나 클라이언트가 프록시로 요청을 보낼 때, 요청줄은 다음과 같은 `완전한 URI`를 갖는다
~~~
    GET http://www.marys-antiques.com/index.html HTTP/1.0
    User-Agent: SuperBrowserv1.3
~~~

: 왜 서버와 프록시가 각각 다른 요청 형식을 갖을까? 원래의 `HTTP 설계`에서 클라이언트는 **단일한 서버**와 대화했다.

: `가상 호스팅`은 존재하지 않았고, 프록시에 대한 대비도 없었다. 따라서 단일 서버는 자신의 `호스트 명`과 `포트번호`를
알고 있으므로, 클라이언트는 불필요한 정보 발송을 피하기 위해 `스킴`, `호스트`, `포트번호`가 없는 `부분 URI`를 보낸 것이다.
> 대리 프록시와 인터셉트 프록시에 `부분 URI`를 받는다.

: 프록시가 부상하면서, 부분 URI는 문제가 되었다. 프록시는 `목적지 서버`와 커넥션을 맺어야하기 때문에,
해당 서버의 이름을 알 필요가 있었다. 그리고 `프록시 기반 게이트웨이`는 FTP 리소스 혹은 그 외의 스킴과 연결하기 위해
`URI의 스킴`을 알 필요가 있었다.

: HTTP/1.0은 프록시 요청의 경우 완전한 URI를 요구하는 것으로 문제를 해결했지만, 서버 요청에 부분 URI는 여전히 남아있다.

: 따라서 우리는 서버로는 `부분 URI`를, 프록시로는 `완전한 URI`를 보낼 필요가 있다. 
클라이언트는 `프록시 설정`에 따라 어떤 URI를 보낼 지 결정할 수 있다.

가상 호스트에서 일어나는 같은 문제
: 프록시의 `스킴/호스트/포트번호 누락` 문제는 가상으로 호스팅 되는 웹 서버가 직면한 것과 같은 문제다.
가상으로 호스팅 되는 웹 서버는 여러 웹 사이트가 **같은 물리적 웹 서버**를 공유한다.

: 요청 하나가 `부분 URI/index.html`로 오면, 가상 호스팅 웹 서버는 그 요청이 접근하고자 하는 웹 사이트의
`호스트 명`을 알 필요가 있다. 이 문제들은 다음과 같은 방법으로 해결되었다.
- 명시적인 프록시는 요청 메시지가 완전한 URI를 갖도록 함으로써 이 문제를 해결했다.
- 가상 호스팅 웹 서버는 호스트와 포트에 대한 정보가 담겨 있는 `Host 헤더`를 요구한다.

인터셉트 프록시는 부분 URI를 받는다
: 클라이언트는 자신이 프록시와 대화하고 있음을 항상 알고 있는 것은 아니다. 
몇몇 프록시는 클라이언트에게 **보이지 않을 수 있기** 때문이다.

: 클라이언트가 프록시를 사용한다고 설정하지 않더라도, 클라이언트의 트래픽은 `대리 프록시`나 `인터셉트 프록시`를 지날 수 있다.
두 경우 모두, 클라이언트는 자신이 웹 서버와 직접 대화하고 있다고 생각할 것이고 `부분 URI`를 보낼 것이다.
> `인터셉트 프록시`는 네트워크 흐름에서 클라이언트-서버로 가는 트래픽을 가로채어 **캐시된 응답**을 돌려주는 프록시 서버이다.
> 인터셉트 프록시는 클라이언트에서 서버로 가는 트래픽을 가로채기 때문에, 요청은 `부분 URI`이다.

프록시는 프록시 요청과 서버 요청을 모두 다룰 수 있다
: 트래픽이 프록시 서버로 **리다이렉트** 될 수 있는 여러 가지 방법이 존재하기 때문에,
`다목적 프록시 서버`는 요청 메시지의 완전한 URI와 부분 URI를 모두 지원해야 한다. 완전 URI와 부분 URI를 사용하는 규칙은 다음과 같다.
    - 완전 URI가 주어졌다면, 프록시는 그것을 사용해야 한다.
    - 부분 URI가 주어졌고 `Host 헤더`가 있다면, Host 헤더를 이용해 원 서버의 `이름`과 `포트번호`를 알아내야 한다.
    - 부분 URI가 주어졌으나 `Host 헤더`가 없다면, 다음의 방법으로 원 서버를 알아내야 한다.
        - 프록시가 `대리 프록시`라면, 프록시에 실제 서버의 `IP 주소`와 `포트번호`가 설정되어 있을 수 있다.
        - 이전에 어떤 `인터셉트 프록시`가 가로챘던 트래픽을 받았고, 그 인터셉트 프록시가 `IP 주소`와 `포트번호`를 사용할 수 있도록
        해두었다면, 그 IP 주소와 포트번호를 사용할 수 있다.
        - 모두 실패했다면, 프록시는 원 서버를 알아낼 수 있는 충분한 정보를 갖고 있지 못한 것이므로 반드시 **에러 메시지**를
        반환해야한다.
        > 에러 메시지는 보통 사용자에게 `Host 헤더`를 지원하는 브라우저로 **업그레이드** 하라는 것이다.

전송 중 URI 변경
: 프록시 서버는 요청 URI의 **변경**에 매우 신경 써야 한다. 
사소한 URI 변경이라도 `다운스트림 서버`와 `상호운용성` 문제를 일으킬 수 있다.
특히 몇몇 프록시는 URI를 `다음 홉`으로 보내기 전에 `표준 형식`으로 **정규화**하는 것으로 알려져 있다.

: 일반적으로 프록시 서버는 **가능한 한 관대**해야 한다. 프로토콜을 엄격하게 준수하도록 강제하는 행위는 기존에 잘 동작하던
기능들을 망가뜨릴 수 있다.

: 특히 HTTP 명세는 일반적인 `인터셉트 프록시`가 URI를 전달할 때 절대 경로를 **고쳐 쓰는 것**을 금지한다.
유일한 예외는 빈 경로를 `'/'`로 교체하는 것 뿐이다.

URI 클라이언트 자동확장과 호스트 명 분석(Hostname Resolution)
: 브라우저는 프록시의 존재 여부에 따라 요청 URI를 다르게 분석한다.
프록시가 없다면 사용자가 타이핑한 URI를 가지고 그에 대응하는 `IP 주소`를 찾는다.
만약 `호스트 명`이 발견되면, 그에 해당하는 IP 주소들을 연결에 **성공할 때까지** 시도해본다.

: 그러나 호스트가 발견되지 않는다면, 많은 브라우저들은 사용자가 호스트 명의 `짧은 약어`를 타이밍한 것으로 보고
`자동화된 호스팅 명의 확장`을 제공하고자 다음과 같이 몇 가지를 시도한다.
    - 일반적인 웹 사이트 이름의 `가운데 부분`만 입력했다면, 많은 브라우저는 `www.` 접두사를 붙이고 `.com` 접미사를 붙인다.
    - 심지어 몇몇 브라우저는 해석할 수 없는 URI를 `서드파티 사이트`로 넘기기도 하는데,
    이 사이트는 오타 교정을 시도하고 사용자가 의도했을 URI를 제시한다.
    - 대부분의 시스템에서 DNS는 사용자 호스트 명의 `앞 부분`만 입력하면 자동으로 도메인을 검색하도록 설정되어 있다.

프록시 없는 URI 분석(URI Resolution)
: 프록시 없는 브라우저 호스팅 명 자동확장은 다음과 같이 이루어진다.
    1. 사용자는 웹 사이트의 `가운데 부분`을 브라우저 URI 창에 입력했다. 브라우저는 이를 `호스트 명`으로 사용하고
    기본 스킴을 `http://`로, 기본 포트를 `80`으로 기본 경로를 `'/'`로 간주한다
    
    2. 브라우저는 호스트 `가운데 부분`을 찾아본다. 이는 실패한다.
    
    3. 브라우저는 호스트 명을 **자동**으로 확장한 후, `DNS 서버`에 `주소 분해(resolve)`를 요청한다. 이것은 성공한다.
    
    4. 이제 브라우저는 `자동 확장된 URI`로 연결하는데 성공한다. 

명시적인 프록시를 사용할 때의 URI 분석
: 명시적인 프록시를 사용하면, 브라우저는 부분 호스트 명을 `자동확장` 하지 않는다. 
브라우저의 URI가 프록시를 **그냥 지나쳐버리기 때문**이다.

: 그 결과, 사용자가 요청 URI는 호스트 명 `가운데 부분`에 `기본 스킴`과 `경로('/')`만 추가될 뿐이다.
> 프록시가 명시적으로 사용되면, 요청은 `완전 URI`으로 보내져야 한다.

: 따라서 몇몇 프록시는 `www..com` 자동확장이나 `지역 도메인 접미사` 추가와 같은 브라우저의 편리한 서비스를
최대한 흉내 내려고 시도한다.

인터셉트 프록시를 이용한 URI 분석
: 호스트 명 분석은 보이지 않는 `인터셉트 프록시`와 함께일 때 달라진다. 클라이언트 입장에서 프록시는 존재하지 않기 때문이다.

: `DNS`가 성공할 때까지 `호스트 명`을 자동확장하는 브라우저를 사용할 때, 동작은 프록시가 아닌 서버의 경우와 별 차이가 없다.
그러나 서버로의 커넥션이 만들어졌을 때는 분명한 차이가 발생한다. 다음은 이와 관련된 트랜잭션의 예이다.
> 인터셉트 프록시를 사용하고 있는 브라우저는 `죽은 서버의 IP 주소`를 탐지할 수 없다.

- 브라우저는 `DNS`를 통해 호스트를 찾아본다. `DNS 서버`는 성공하고 IP 주소를 브라우저에 반환한다. 이 과정까지는 차이가 없다.
- 서버로의 커넥션이 생성된 후, 클라이언트는 모든 IP 주소에 **접속**을 시도한다. 어떤 IP 주소들이 죽은 것일 수 있다.
그러나 `인터셉트 프록시`와 함께라면, `첫 번째 접속 시도`는 원 서버가 아닌 프록시 서버에 의해 종료된다.
- 클라이언트는 성공적으로 웹 서버와 대화했다고 믿지만, 웹 서버는 살아있지도 않았을 것이다.
- 프록시가 최종적으로 진짜 원 서버와 상호작용할 준비가 되었을 때, 프록시는 해당 IP 주소가 실제로는 `다운된 서버`를 가리키고
있음을 알게 될 것이다.
- 브라우저에서 제공하는 것과 동등한 수준의 `장애 허용(fault tolerance)`을 제공하기 위해서, 
프록시는 `Host 헤더`에 들어 있는 호스트 명을 다시 분석하든, 아니면 IP 주소에 대한 `역방향 DNS 룩업`을 해서든
다른 IP 주소에 접속을 시도해야 한다.
- 인터셉트 프록시와 명시적인 프록시 모두 `죽은 서버의 DNS 분석에 대한 장애 허용`을 지원해야 한다는 것이 중요하다.
브라우저가 명시적인 프록시를 사용하도록 설정되어 있는 경우의 `장애 허용`은 프록시에 달려있기 때문이다.
> `장애 허용(fault tolerance)`이란, 장애가 발생하더라도 여분의 시스템 구성 요소를 제공하여 
데이터 무결성과 시스템의 기능을 보장하는 특성이다.

## 메시지 추적
---
오늘날, 웹 요청이 클라이언트에서 서버로 향하는 도중에 둘 이상의 프록시를 지나게 되는 것은 흔한 일이다.
동시에 성능상의 이유로 세계 곳곳에 흩어져 있는 `대리 캐시 저장소`에 컨텐츠를 복제해두는 방식이 점점 더 흔해지고 있다.

프록시는 여러 벤더에 의해 개발된다. 그들은 서로 다른 기능과 버그들을 갖고 있으며 여러 조직에 의해 관리된다.

프록시가 점점 흔해지면서, 서로 다른 `스위치`와 `라우터`를 넘나드는 IP 패킷의 흐름을 추적하지 못하는 것 못지않게
프록시를 넘나드는 **메시지의 흐름을 추적**하고 문제점을 찾아내는 것도 필요한 일이 되었다.

Via 헤더
: `Via 헤더 필드`는 메시지가 지나는 각 중간 노드(`프록시`, `게이트웨이`)의 정보를 나열한다.
메시지가 또 다른 노드를 지날 때마다, 중간 노드는 `Via 목록`의 끝에 반드시 추가되어야 한다.

: 다음의 Via 문자열은 메시지가 두 개의 프록시를 지나갔음을 말해준다. 이 문자열에 따르면 첫 번째 프록시는
`HTTP/1.1` 프로토콜을 구현했으며 `proxy-62.irenes-isp.net`라 불리고, 두 번째 프록시는 `HTTP/1.0`을 구현했고
`cache.joes-hardware.com`라 불린다.
~~~
    Via 1.1 proxy-62.irenes-isp.net, 1.0 cache.joes-hardware.com
~~~

: `Via 헤더 필드`는 메시지의 전달을 추적하고, 메시지 루프를 진단하고, 요청을 보내고 그에 대한 응답을 돌려주는
과정에 관여하는 `모든 메시지 발송자들의 프로토콜`을 다루는 능력을 알아보기 위해 사용된다.

: 프록시는 또한 네트워크의 `라우팅 루프`를 탐지하기 위해 Via 헤더를 사용할 수 있다. 프록시는 요청을 보내기 전에
자신을 가리키는 `유일한(unique) 문자열`을 Via 헤더에 삽입해야 하며, 네트워크에 라우팅 루프가 있는지 **탐지하기 위해**
이 문자열이 들어온 요청이 있는지 검사해야 한다.

Via 문법
: Via 헤더 필드는 쉼표로 구분된 `경유지(waypoint)`의 목록이다. 각 경유지는 `개별 프록시 서버`나 `게이트웨이 홉`을 나타내며
그들 중간 노드의 프로토콜과 주소에 대한 정보를 담고 있다.

: 각 `Via Waypoint`는 `프로콜 이름(선택. 기본 HTTP)`, `프로토콜 버전(필수)`, `노드 이름(필수)`, `노드 코멘트(선택)`
최대 4개의 구성요소를 담을 수 있다.

: `노드 이름`에는 중개자의 `호스트`와 `포트번호`를 기입한다. 정보 보호를 이유로 진짜 호스트 명을 숨기고 싶어할 수 있는데,
이러한 경우에는 `가명`으로 대체할 수 있다.

: `노드 코멘트`는 중개자 노드를 서술하는 선택적인 코멘트다. `벤더`나 `버전 정보`를 여기에 포함시키는 것은 흔한 일이며,
몇몇 프록시 서버는 장치에서 일어난 이벤트에 대한 **진단 정보**를 포함하는 데도 코멘트 필드를 사용한다.

Via 요청과 응답 경로
: 요청 메시지와 응답 메시지 모두 프록시를 지나므로 둘 모두 Via 헤더를 가진다.
`응답 Via 헤더`는 거의 `요청 Via 헤더`와 반대이다.

Via와 게이트웨이
: 몇몇 프록시는 서버에게 `비 HTTP 프로토콜`을 사용할 수 있는 게이트웨이 기능을 제공한다. Via 헤더는 이러한 **프로토콜 변환**
을 기록하므로, HTTP 애플리케이션은 프록시 연쇄에서 **프로토콜 능력과 변환**이 있었는지를 알 수 있다.

Server 헤더와 Via 헤더
: `Server 응답 헤더` 필드는 원 서버에 의해 사용되는 소프트웨어를 알려준다. 응답 메시지가 프록시를 통과할 때,
프록시는 Server 헤더를 **수정해서는** 안 된다. `Server 헤더`는 원 서버를 위해 존재한다. 대신 프록시는 Via 항목을 추가해야 한다.

Via가 개인정보 보호와 보안에 미치는 영향
: Via 문자열 안에 `정확한 호스트 명`이 들어가기를 원하지 않는 몇 가지 경우가 있다.
- 명시적으로 이 동작이 켜져 있지 않는 이상, 프록시 서버가 네트워크 방화벽의 일부인 경우 프록시는 **방화벽 뒤에 숨어있는**
`호스트 명`과 `포트 번호`를 전달해서는 안 된다.
- 만약 `Via 노드 이름` 전달이 가능하지 않다면, 보안 경계선의 일부분인 프록시는 `호스트 명`을 그 호스트에 대한
적당한 가명으로 교체해야 한다. 이로 인해 실제 이름을 알기 어렵다고 하더라도, 프록시는 각 프록시 서버에 대한
`Via 경유지` 항목을 유지하려고 노력해야 한다.
- `내부 네트워크 아키텍쳐의 설계`와 `토폴로지`를 알아내기 어렵게 하기 위해 아주 강력한 보안 요구사항을 갖고 있는 조직을 위해,
프록시는 정렬된 일련의 `Via 경유지` 항목들을 하나로 합칠 수 있다.
- 단, 경유지들이 모두 같은 조직 통제하에 있고 호스트가 가명이
아니면 합쳐서는 안 된다. 또한, 수신된 프로토콜 값이 서로 다른 항목도 합쳐서는 안 된다.

> `토폴로지`란, 컴퓨터 네트워크의 요소들(`링크`, `노드` 등)을 물리적으로 연결해 놓은 것, 또는 그 연결 방식을 말한다. 
> `로컬 영역 네트워크(LAN)`은 물리적 토폴로지와 논리적 토폴로지 **둘 다** 보여 줄 수 있는 네트워크의 한 예이다.

Trace 메서드
: `프록시 서버`는 메시지가 전달될 때 메시지를 바꿀 수 있다. 헤더가 `추가`, `변경`, `삭제`될 수 있고, 본문이 다른 형식으로
변환될 수 있다.

: 프록시가 점점 **더 복잡**해지고 벤더가 **더 많은** 프록시를 배치하면서, 프록시의 `상호운용성` 문제가 증가한다.

: 이러한 프록시 네트워크를 쉽게 진단하기 위해 우리는 `HTTP 프록시 네트워크`에서 `홉에서 홉`으로 전달될 때 마다 **메시지의 내용**이
어떻게 변하는지 관찰하는 방법이 필요하다.

: HTTP/1.1의 `TRACE` 메서드는 요청 메시지를 프록시의 연쇄를 따라가면서 어떤 프록시를 지나가고,
어떻게 각 프록시가 요청 메시지를 수정하는지 **추적**할 수 있도록 해준다. 이는 프록시 흐름을 `디버깅`하는데 매우 유용하다.

: TRACE 요청이 `목적지 서버`에 도착했을 때, 서버는 `전체 요청 메시지`를 HTTP 응답 메시지 본문에 포함시켜 송신자에
그대로 돌려보낸다. 

: TRACE 응답이 도착했을 때, 클라이언트는 서버가 받은 `메시지`와, `Via 헤더`를 검사할 수 있다. TRACE 응답의
`Content-Type`은 `message/http`이며, 상태 코드는 `200 OK`이다.

Max-Forwards
: 일반적으로 `TRACE 메시지`는 중간에 프록시들이 몇 개나 있든 **신경 쓰지 않고** 목적지 서버로의 모든 경로를 여행한다.
`TRACE`와 `OPTIONS` 요청의 `홉(hop)` 갯수를 제한하기 위해 `Max-Forwards` 헤더를 사용할 수 있다.

: 이는 전달되는 메시지가 `무한 루프`에 빠지지 않는지 프록시 연쇄를 테스트하거나, 연쇄 중간의 특정 프록시 서버의 효과를
체크할 때 유용하다.
> `Max-Forwards: 0`이면, 수신자는 자신이 원 서버가 아니라 할지라도 `TRACE` 메시지를 더 이상 전달하지 않고 클라이언트로
돌려준다.

## 프록시 인증
---
프록시는 `접근 제어 장치`로서 제공될 수 있다. HTTP는 사용자가 유효한 `접근 권한 자격`을 프록시에 제출하지 않는 한 `컨텐츠에
대한 요청`을 **차단**하는 `프록시 인증`이라는 메커니즘을 정의하고 있다.
- 제한된 컨텐츠에 대한 요청이 프록시 서버에 도착했을 때, 프록시 서버는 접근 자격을 요구하는 `407 Proxy Authorization Required`
상태 코드와, 그 자격을 제출하는 법을 설명해주는 `Proxy-Authenticate` 헤더 필드를 함께 반환 할 수 있다.

- 클라이언트는 `407 응답`을 받게 되면, 로컬 데이터베이스를 확인해서든 사용자에게 물어봐서든 **요구되는 자격**을 수집한다.

- 자격을 획득하면, 클라이언트는 요구되는 자격을 `Proxy-Authorization` 헤더 필드에 담아서 요청을 다시 보낸다.

- 자격이 유효하다면, 프록시는 원 요청을 **연쇄**를 따라 통과 시킨다. 그렇지 않다면 `407 응답`을 보낸다.

## 프록시 상호운용성
---
`클라이언트`, `서버`, `프록시`는 HTTP 명세의 여러 `버전`과 `벤더`에 의해 만들어진다.
그렇기에 프록시 서버는 **서로 다른 프로토콜**을 구현했을 수도 있고, 이상한 동작을 하는 클라이언트와 서버를 중개해야 한다.

지원하지 않는 헤더와 메서드 다루기
: 프록시 서버는 넘어오는 헤더 필드들을 모두 이해하지 **못할** 수도 있다.
몇몇 헤더는 프록시 자신보다 새로운 것일수도 있고, 특정 애플리케이션만을 위해 만들어진 것일 수도 있다.

: 프록시는 이해할 수 없는 헤더 필드는 반드시 **그대로 전달**해야 하며, 같은 이름의 헤더 필드가 여러 개 있는 경우에는
그들의 `상대적인 순서`도 반드시 유지해야 한다. 지원하지 않는 메서드 또한 `다음 홉`으로 넘겨줘야 한다.

OPTIONS: 어떤 기능을 지원하는지 알아보기
: HTTP `OPTIONS` 메서드는 서버나 웹 서버의 특정 리소스가 **어떤 기능을 지원**하는지 클라이언트(혹은 프록시)가
알아볼 수 있게 해준다.

: OPTIONS 요청의 URI가 `별표(*)`라면, 요청은 서버 전체의 능력에 대해 묻는 것이 된다.
~~~
    OPTIONS * HTTP/1.1
~~~

: 만약 URI가 `실제 리소스`라면, OPTIONS 요청은 특정 리소스에 대해 가능한 기능들을 묻는 것이다.
~~~
    OPTIONS http://www.joes-hardware.com/index.html HTTP/1.1
    static HTML file woudn't accept a POST method
~~~

: 요청이 성공한다면, 지정한 리소스가에 대해 **가능한 기능**들을 서술하는 헤더 필드와 `200 OK` 응답을 반환한다.

: 하지만 `HTTP/1.1`이 명시한 헤더는 서버에 의해 어떤 메서드가 지원되는지 서술하는 `Allow 헤더` 하나 뿐이다.
더 많은 정보를 위해 **선택적인** 응답 본문을 허용하지만, 이에 대해 정의된 것은 없다.

Allow 헤더
: `Allow 엔터티 헤더` 필드는 요청 URI에 의해 식별되는 자원에 대해 지원되는 `메서드`나, 서버가 지원하는 모든 `메서드`를
열거한다.
~~~
    Allow: GET, HEAD, PUT
~~~

: `Allow 헤더`는 새 리소스가 지원했으면 하는 메서드를 추천하기 위해 `요청 헤더`로 사용될 수 있다.
서버는 추천 받은 메서드를 모두 지원해야 할 **의무**는 없으며, 그 요청에 대한 응답에는 Allow 헤더를 포함시켜야 한다.

: 만약 프록시가 지정된 모든 메서드를 이해할 수 없다고 해도, 프록시는 `Allow 헤더` 필드를 수정할 수 없다.
클라이언트가 원 서버와 대화하는 **다른 경로**를 갖고 있을 수도 있기 때문이다.