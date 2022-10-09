# 프로메테우스를 통한 Infra Structure Monitoring

```
21.10.22 - 업무에 도입할 모니터링 툴을 찾는 여정입니다. 이후 변경이나 수정된 내용이 있을 수 있습니다.
```

🔥 업무와 관련하여 임베디드 Infra 레벨에서는 각 제어보드의 상태를 모니터링하고 원격으로 관리하는 효율적인 방안이 필요함. 전체 Infra Structure의 내부가 아닌, 외부에서 시스템을 모니터링하는 방안을 모색하던 중 프로메테우스를 알게되었고 이를 소개 하고자 함.





<br/>



관련 링크 : [스프링+프로메테우스](https://github.com/t0e8r1r4y/springframewordk/tree/main/prometheus_spring)

<br/>
---

## 1. 프로메테우스란?


💡 [Prometheus](https://github.com/prometheus) is an open-source systems monitoring and alerting toolkit originally built at [SoundCloud](https://soundcloud.com/). Since its inception in 2012, many companies and organizations have adopted Prometheus, and the project has a very active developer and user [community](https://prometheus.io/community). It is now a standalone open source project and maintained independently of any company. To emphasize this, and to clarify the project's governance structure, Prometheus joined the [Cloud Native Computing Foundation](https://cncf.io/) in 2016 as the second hosted project, after [Kubernetes](https://kubernetes.io/).

Prometheus collects and stores its metrics as time series data, i.e. metrics information is stored with the timestamp at which it was recorded, alongside optional key-value pairs called labels.



`모니터링 및 경보를 보내주는 toolkit이다.`

## 2. 프로메테우스의 사용 목적 → 모니터링

### 모니터링이란?

- 모니터링이란 쉽게 설명하면, 운영하는 시스템이 정상적으로 동작하는지 여부를 체크하기 위해서 시스템의 리소스나 동작중인 프로그램의 로그등을 수집하고 분석하는 행위
- 프로메테우스로 모니터링이 가능한 시스템이라고함은 최소 OS가 설치되어 구동되는 시스템이라고 할 수 있다.

### 모니터링을 정의하는 요소

- 모니터링은 대게 아래의 3가지 요소 정도로 상황이 정의 된다.
    - 데이터 해상도 ( 가령 고해상도라고 하면 동일 시간 내에 더 많은 시계열 데이터를 가진다는 의미 )
    - 지연 시간
    - 데이터 다양성

### 모니터링 구성요소

- 메트릭 ( Metrics ) : 특정 시스템의 리소스 정보를 시계열 형태로 표출하는 형태. 표출은 특정 시점에서 수치로 표출 됨
    
    <aside>
    💡 In layperson terms, metrics are numeric measurements, time series mean that changes are recorded over time. What users want to measure differs from application to application. For a web server it might be request times, for a database it might be number of active connections or number of active queries etc.
    
    Metrics play an important role in understanding why your application is working in a certain way. Let's assume you are running a web application and find that the application is slow. You will need some information to find out what is happening with your application. For example the application can become slow when the number of requests are high. If you have the request count metric you can spot the reason and increase the number of servers to handle the load.
    
    </aside>
    
- 로깅 ( Logging ) : 메트릭보다 더 세부적인 데이터를 포함하는 시스템이나 애플리케이션의 이벤트로 나타남
- 추적 ( Tracing ) : 요청이 모든 시스템에 걸쳐 전체 라이프사이클 동안 추적 될 수 있도록 고유한 식별자를 제공하는 로깅의 특별한 경우
- 알림 ( Alerting ) : 메트릭이나 로그의 지속적인 임계값의 유효성을 검사하며 임계값을 위반하는 경우 통지
- 시각화 ( Visualization ) : 시각 자료 형태, 주로 그래프 형태

### 모니터링 방법

- 화이트 박스 :  타겟 시스템의 내부에서 주요 성능에 대한 데이터를 제공 → 프로메테우스는 여기에 해당
- 블랙박스 : 시스템 외부에서 타겟 시스템의 응답을 검사

### 메트릭 수집 방식

- Pull Based
    - 클라이언트에서 이벤트가 발생하게 되면 클라이언트는 서버로 이벤트가 있음을 알리고, 이를 send하는 버퍼의 엔드포인트에 저장. 서버는 이벤트 initialize 요청을 수신하고 엔드포인트로부터 데이터를 가져옴
    - 프로메테우스 아키텍처에서 보면 타겟 애플리케이션의 Exporter EndPoint로 부터 데이터를 scrape하는 방식
    - 모니터링 설정을 server에서 하므로 관리가 집중 됨
    - 받는 쪽(서버)에서 장애가 생겨도 타겟 어플리케이션에 장애가 발생하지 않음
    - 프로메테우스는 Pull 방식을 채택 함
    - Zabbix, Zenoss, Sensu 등이 이를 채택
- Push Based
    - 등록 된 서버에서 원하는 타이밍에 원하는 내용을 수신 받을 수 있도록 클라이언트가 서버로 메트릭을 전송하는 방식
    - 모니터링의 설정이 client에 있어 관리가 분산 됨
    - 받는 쪽(서버)에서 장애가 생기면 타겟 어플리케이션에 장애가 발생할 수 있음
    - 장점은 서비스가 오토스케일링 등 가변적으로 변동이 생기는 상황에 유리함
    - Elasticsearch, LogStash, Kibana 등은 이를 채택

<aside>
💡 나의 견해
어떤 방식을 사용하느냐는 어떤 시스템에서 어떤 데이터를 핸들링 할 것인가에 대한 문제임
가령 push방식을 150Hz이상의 데이터가 발생되는 클라이언트에 연결한다고 치고, raw데이터를 수집한다고하면 서버가 견디기 위해서 많은 리소스 투입이 필요함. 이럴 경우 필요한 데이터면 scrape 해가는 것이 모니터링 시스템에 영향이 더 적음
반대로 이렇게 되면 특정 시점을 캡쳐하는 것이므로 모든 데이터에 대해서 감시는 어려울 수 있으며, 특정 상황에서 돌발적으로 발생하는 장애를 감시하기는 어려움
반대의 경우도 그런 케이스라고 생각 됨.

</aside>

### 모니터링 메트릭의 분류 ( 모니터링 대상의 Level에 따른 구분 )

- 인프라 수준의 메트릭
    - 호스트 레벨에서의 메트릭
    - 호스트에서 사용 중인 파일 디스크립터의 갯수, 디스크 사용량, NIC에서의 패킷 전송량
    - node-exporter는 인프라 수준의 메트릭 도구
- 컨테이터 수준의 메트릭
    - 컨테이너 레벨에서의 메트릭
    - 컨테이너별 CPU관리와 메모리 사용량, 컨테이너 프로세스의 상태, 컨테이너에 할당된 리소스 할당량
    - Cadvisor는 컨테이너 수준의 메트릭 도구
- 애플리케이션 수준의 메트릭
    - 인프라, 컨테이너를 제외한 메트릭
    - MSA에서 발생하는 트레이싱 데이터, 애플리케이션 로직에 종속적인 데이터, 서버 프레임워크에서 제공하는 모니터링 데이터

### 모니터링 메트릭의 구분 ( 프로메테우스에서 모니터링 방법 )

- Counter 매트릭 : 시간이 지남에 따라 점점 숫자가 누적되어 전체적으로 증가하는 모델
- Gauge 매트릭 : 값이 증가하거나 감소를 반복하는 데이터에 적합한 매트릭
- Histogram 매트릭 : 응답  크기, 요청 기간 등 start ~ end 주기 내에서 값의 증감을 관찰하고, 전체 합계를 모두 확인할 수 있는 매트릭
- Summery 매트릭 : 보통 잘 안쓴다고 함. 설명은 히스토릭과 동일

## 3. 프로메테우스 아키텍처 개요

![Untitled](https://user-images.githubusercontent.com/91730236/194733309-7f0515f1-5211-4592-9b55-f0f305dca295.png)

> 동작을 3줄로 요약하자면
1. 모니터링 대상 시스템에 설치 된 Exporter로(Client) 부터 설정 된 작업에 대한 메트릭 정보를 수집. 
2. 수집 된 정보는 프로메테우스 서버에서 시계열 형태의 데이터로 수집
3. 데이터 시각화(PromQL 사용) 및 경고 표시
> 

### 프로메테우스 아키텍처의 특징

- a multi-dimensional [data model](https://prometheus.io/docs/concepts/data_model/) with time series data identified by metric name and key/value pairs
- PromQL, a [flexible query language](https://prometheus.io/docs/prometheus/latest/querying/basics/) to leverage this dimensionality
- no reliance on distributed storage; single server nodes are autonomous
- time series collection happens via a pull model over HTTP → 위에서 언급한 Pull 방식
- [pushing time series](https://prometheus.io/docs/instrumenting/pushing/) is supported via an intermediary gateway
- targets are discovered via service discovery or static configuration → 서버에서 static config 관리를 하던지 service discovery를 활용하던지
- multiple modes of graphing and dashboarding support → 그라파나 이런것들 지원된다.

### 메트릭과 라벨의 구조와 PromQL

```markdown
<metric name>{<label name>=<label value>, ...}

// 요청 시
http_requests_total{method="POST", handler="/dir"}
```

- 메트릭 네임과 각각의 라벨들이 키/밸류 구조로 짝을 이루고 있음 → 이는 PromQL 프로메테우스 쿼리 사용의 가장 기본 형태가 됨
- <메트릭 이름>{<레이블 키>=<레이블 값>, <레이블 키>=<레이블 값> ...} <메트릭 값> [<timestamp>]

- PromQL : 프로메테우스 쿼리 랭귀지의 약자로 시계열 데이터베이스 처리를 제대로 할 수 있는 독자적인 DB 쿼리를 가지고 있음
- PromQL의 문법은 아래 블로그에 잘 설명이 되어있고, Hands-On에서 조금 더 다룰 예정

[Prometheus Query(PromQL) 기본 이해하기](https://devthomas.tistory.com/15)

### 동작원리

![Untitled 1](https://user-images.githubusercontent.com/91730236/194733323-a5f0a2e9-9c16-44fc-8cfb-13072bba857c.png)

( 프로메테우스를 이해하는 내내 공식 사이트에서 제공한 것 보다 이게 더 잘 이해가 됨.... )

- 메트릭 수집 부분
    - 도식 : Target System과 Exporter 그리고 pulling 방식 까지
    - 수집 대상이 Target System. 다양한 예제들을 살펴보면 결국 하나의 OS가 구동이 가능한 EC2, VM에서 생성 된 하나의 머신, 쿠버네티스의 컨테이너 등이 그 대상이 됨을 쉽게 알 수 있음
    - 풀링 방식 : 프로메테우스가 Exporter에서 메트릭을 스크랩하여 수집하는 방식
- 서비스 디스커버리
    - 도식 : Service Discovery
    - 풀링 방식의 단점을 보완하기 위한 방법
    - 위 pulling 방식에 대한 설명에서 프로메테우스는 서버가 모니터링 대상에 대한 config를 정의한다고 하였음. 이런 경우 각각의 tartget 서비스들이 오토 스케일링이 되는 상황에서 증가 된 서비스를 별도 config하지 않는다면 모니터링을 못함
    - 그럴 경우 이런 service discovery를 적용하여 변동되는 부분에 대해 체크를하고 기동중인 서비스의 목록과 IP 목록만 들고 있으면 이를 서버가 조회하기 위해서 서비스 디스커버리가 필요함
- Exporter와 Retrieval
    - Exporter는 서버가 target system에서 데이터를 읽어가는 부분
    - Exporter는 단순히 HTTP Get으로 매트릭을 텍스트 형태로 리턴 ( 히스토리 저장 X )
    - Retrieval는 주기적으로 메트릭을 수집하는 모듈
- Strage
    - 서버의 물리적으로 디스크와 로컬에 저장
    - 로컬 저장방식은 설치가 쉽다는 장점이 있지만, 데이터 저장량이 증가하면 스케일링이 불가능하다는 단점 → 물리적 저장 공간을 증설. 어떤 사람은 프로메테우스 서버를 여러개 두던데... 이것을 실제로 구현하려면 모니터링 대상의 메트릭을 정확히 측정하여 분산 설계자체가 중요해 질 듯.
    - 이걸 또 해결하기위해서 Thanos라는 오픈 소스를 사용
- PromQL
    - 저장 된 메트릭을 조회하귀 위한 프로메테우스 자체적인 쿼리 언어
    - 이를 통해 그라파나 등과 통합하여 데이터 시각화가 가능함

### 프로메테우스 적용 시 주의 사항

- pulling 방식의 단점인데, 결국 exporter에서 가져오는 것이므로 그 순간의 스크랩 데이터일 뿐, 연속적인 흐름을 쭉 보는게 아니라는 것. 이를 감안하여 모티링이 필요함
- 메트릭 저장 공간에 대한 이슈. → 자동 확장이 어렵다. → 결국 메트릭 데이터를 주기적으로 외부로 빼내든지, 아니면 물리적 저장 공간 증설이 계속 이루어 져야함.

## 4. 간단한 구동

- 아래 링크에 나오는 내용들을 해보고 있는 중 → 적용 해보고 결과를 공유하고자 함
- 그리고 개인적으로 매번 이런 툴을 사용하며 아쉬운 점은... 이런 환경에서 동작시킬 application의 부재가 실제 성능을 체크하는데 뭔가 아쉬움
- 아래 [영상](https://www.youtube.com/watch?v=JWdQp6VrMOw&list=WL&index=4) 채택 이유는 스프링 부트에서 시간이 될 때 간단한 application 개발을 동반하기 위함
- [개인적으로 적용해본 경험](https://github.com/t0e8r1r4y/springframewordk/tree/main/prometheus_spring)



---
참고자료
| 제목 | 설명 | 링크 |
| --- | --- | --- |
| 프로메테우스 인프라스트럭처 모니터링 | 도서입니다. | pdf 개인 소장 |
| 공식사이트 | 프로메테우스 공식 사이트입니다. | [링크](https://prometheus.io) |
| 오픈소스 | 프로메테우스 git 오픈소스입니다. | [링크](https://github.com/prometheus/docs#contributing-changes)|
