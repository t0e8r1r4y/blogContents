<h1 align="center">
  <br>
  <img src="https://learn.microsoft.com/ko-kr/azure/architecture/patterns/_images/command-and-query-responsibility-segregation-cqrs-basic.png"  width=600"></a>
  <br>
  <br>
    CQRS에 패턴
  <br>
  <br>
</h1>



# CQRS란

## 정의

CQRS는 데이터 저장소에 대한 읽기 및 업데이트 작업을 구분하는 패턴인 명령 및 쿼리 책임분리를 의미한다.
어플리케이션에서 CQRS를 구현하면 성능, 확장성 및 보안을 최대화할 수 있습니다.
CQRS로 마이그레이션하면 유연성이 생기므로 시스템이 점점 진화하고 업데이트 명령이 도메인 수준에서 병합 충돌을 일으키지 않도록 할 수 있음.


<br/>

## :link: 관련 내용 내가 정리한 링크
| 제목 | 링크 | 
| ------ | ------ |
| CQRS란 | [link][내블로그1] |

<br/>

## :rainbow: CQRS 패턴 구현
| Repo | 내용 | 링크 | 
| ------ | ------ | ------ |
| delivery-food-service | NestJS 프로젝트에 CQRS 패턴 적용 | [link][타입스크립트프로젝트1] |
                                                                         
<br/>

## :link: 참고자료
                                                                         
| 출처 | 제목 | 링크 | 
| ------ | ------ | ------ |
| MS-Doc | CQRS 패턴 | [link][CQRS_MSDOC] |
                                                                         
---
**Thanks!**

[//]: # (These are reference links used in the body of this note and get stripped out when the markdown processor does its job. There is no need to format nicely because it shouldn't be seen. Thanks SO - http://stackoverflow.com/questions/4823468/store-comments-in-markdown-syntax)
   [CQRS_MSDOC]: <https://www.mongodb.com/>
   [내블로그1]: <https://medium.com/@tas.com/cqrs%EB%9E%80-%EA%B0%9C%EB%85%90%EC%A0%81%EC%9D%B8-%EB%B6%80%EB%B6%84-%EC%A0%95%EB%A6%AC-d52020f25>
   [타입스크립트프로젝트1]: <https://github.com/t0e8r1r4y/delivery-food-service>
