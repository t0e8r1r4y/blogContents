# GraphQL

## 1. GraphQL이란

[GraphQL: API를 위한 쿼리 언어](https://graphql-kr.github.io/learn/)

### 1-1. 개념

- 페이스북에서 만든 쿼리 언어( 2012년 개발, 2015년 공개 )
- REST를 대체할 수 있음
- 단일 API 호출로 다양한 데이터 소스에서 데이터를 끌어오는 구성할 수 있도록 지원
- Layer7의 HTTP POST 메서드와 웹소켓 프로토콜을 활용함.
- 필요에 따라서는 Layer4의 TCP/UDP를 활용하거나 Layer2 형식의 이더넷 프레임을 활용 가능함

### 1-2. 용어

- 쿼리와 변형
    - 쿼리 : R → 쿼리(Query)
    - 변형 : CUD → 뮤테이션(Mutation)
    - Thrird Operation Type : GraphQL subscriptions ( Event Driven Architecture )
- 스키마 : 쿼리할 가능성 있는 모든 데이터에 대한 설명
    
    <aside>
    👇🏽 Your GraphQL server uses a **schema**
     to describe the shape of your available data. This schema defines a hierarchy of **types** with **fields** that are populated from your back-end data stores. The schema also specifies exactly which **queries** and **mutations** are available for clients to execute.
    
    </aside>
    
- 리졸버 :  ****a function that's responsible for populating the data for a single field in your schema → 스키마의 필드에 대한 데이터를 채우는 함수
- introspection : 스키마가 어떤 쿼리를 지원하는지에 대한 정보를 요청할 수 있는 시스템

### 1-3. 등장 ( 무엇을 해결하고자 하는 기술인가? )

![Untitled](https://user-images.githubusercontent.com/91730236/195039933-8c49118b-1bec-4516-8bfd-c0e9c4d935b1.png)

- 데이터를 효율적으로 가져오는 것을 목표 → REST API의 데이터 유연성 부족을 해결한다.
    - 오버패칭 : 필요하지 않은 데이터까지 받아오는 것을 의미. REST API의 N+1 문제를 해결 할 수 있음
    - 언더패칭 : 필요한 정보를 여러번 요청해야 얻을 수 있을 경우
    - 유연성 부족 : e2e 관리가 필수적이고 규모가 커질수록 관리가 힘듬

<aside>
☝🏾 엔드포인트가 다수로 나뉘어 있기에 위의 문제들이 발생함

</aside>

### 1-4. 동작원리 ( 어떻게 해결하는가 ? )

![Untitled 1](https://user-images.githubusercontent.com/91730236/195039957-222891e5-0db9-4952-a70c-403373a8a6c1.png)

<aside>
👇🏽 GraphQL은 단일 지점 ( 위 예시에서는 Apollo Engine )을 통해 처리하며 그래프 계층 구조를 사용하여 관계를 정의함으로서 유연성을 확보한다.

</aside>

- Backend에서는 클라이언트가 요청할 수 있는 데이터의 타입들과 필드들을 정의한 타입시스템을 구축
- 타입의 각 필드에 대한 요청을 해석 및 처리하는 로직을 Resolver 함수들로 구현
- 클라이언트에서 쿼리를 보내면 Apollo Engine과 같은 구현체에서 쿼리를 검증
- 검증 후 문제가 없다면 query를 실행한 결과를 클라이언트에 전달.

### 1-5. 반대급부

- 단일 지점 장애 발생 이슈
- 재사용 최적화 ( **[persisted-queries](https://github.com/apollographql/apollo-link-persisted-queries) 등 대안이 있기는 함 )**
- 클라이언트 입장에서도 데이터 스키마를 알아야 함.
- 전체 시스템 아키텍처에 부적합한 경우가 있을 수 있음.
- 코드 증가 ( Rest API 대비 )
- 성능 최적화 ( ORM에서 발생하는 N+1 문제 등 )

<br/>
---


## 2.  Hands-On
- 타입스크립트에 GraphQL 적용
