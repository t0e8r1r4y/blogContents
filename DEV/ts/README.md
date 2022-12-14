<h1 align="center">
  <br>
  <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/4/4c/Typescript_logo_2020.svg/220px-Typescript_logo_2020.svg.png"  width=200"></a>
  <br>
  <br>
  TypeScript & NestJS 빠르게 익히기
  <br>
  <br>
</h1>


## 소개

이 레포지토리는 TypeScript와 NestJS를 사용하면서 관련 내용을 정리합니다. C언어와 달리 객체지향적 특성과 그에 따른 설계 패턴, TDD를 체득하기 위한 과정으로 차후에 참고하고자 자료를 수집합니다. 
직접 작성한 글과 링크를 일단 두서 없이 정리 중

## 목차

1. **[타입스크립트](#1-타입스크립트)**
1. **[NestJS](#2-nestjs)**



## 1. 타입스크립트
| TITLE | LINK | SUMMERY | 
| ------ | ------ | ------ |
| Docs | [링크][TS_DOC] | TS Document |
| Docs | [한국어 번역][TS_DOC_KR] | TS Document |
| HandsBook | [핸드북][TS_HAND_BOOK] | 타입스크립트 핸드북 |
                                                                                                                                              
                                                                                                                                              

## 2. NestJS
| TITLE | LINK | SUMMERY | 
| ------ | ------ | ------ |
| 공식 레포 | [nest git][NESTJS_OFFICIAL] | NestJS Open Source |
| Nest.js는 실제로 어떻게 의존성을 주입해줄까? | [coaley님 블로그][NESTJS_INJECTION] | DFS로 모듈을 찾아 토큰 정보를 기반으로 실제 인스턴스를 생성하여 의존성을 관리하더라 |
| NestJs로 배우는 백엔드 프로그래밍 | [wikibook][GITBOOK_NESTJS] | 관심사 분리 방법과 클린 아키텍처에 대한 소개가 좋음 |
| API with NestJS | [WANAGO.IO][WANAGO_NEST] | NestJS에서 많이 쓰이는 부분에 대해서 주제별 정리가 잘 됨 |
| Custom Decorator | [ZOOM 기술블로그][TS_CUSTOM_DECO] | 줌 기술블로그에서 커스텀 데코레이터 제작과 관련된 글을 잘 정리함 |
| Nest.Js Step by Step | [codemag][TS_STEP_LINK] | 기본 세팅과 구성에 대해서 정리가 잘 되어있음 |
| NodeJS Event Loop | [직방기술블로그][NODE_JS_LINK] | NestJS의 기반이 되는 NodeJs 엔진에 대한 내용입니다. |
| Nestjs vs spring | [biud436][NODEVSSPRING_LINK] | NestJs와 Spring framework에 대한 비교글입니다. |
| NestJS Document | [애니띵님블로그][ANYTHING_BLOG] | 나중에 내가 한 NestJS 정리할 때 참고 할 목적 |
| Swagger NesgJS | [git][RYANSIN_BLOG] | Swagger 적용 참고 |


---
**Thanks!**

[//]: # (These are reference links used in the body of this note and get stripped out when the markdown processor does its job. There is no need to format nicely because it shouldn't be seen. Thanks SO - http://stackoverflow.com/questions/4823468/store-comments-in-markdown-syntax)
   [NESTJS_INJECTION]: <https://velog.io/@coalery/nest-injection-how>
   [NESTJS_OFFICIAL]: <https://github.com/nestjs/nest>
   [GITBOOK_NESTJS]: <https://wikidocs.net/book/7059>
   [WANAGO_NEST]: <https://wanago.io/2020/05/11/nestjs-api-controllers-routing-module/>
   [TS_DOC]: <https://www.typescriptlang.org/ko/>
   [TS_DOC_KR]: <https://radlohead.gitbook.io/typescript-deep-dive/>
   [TS_HAND_BOOK]: <https://joshua1988.github.io/ts/>
   [TS_CUSTOM_DECO]: <https://zuminternet.github.io/nestjs-custom-decorator/>
   [TS_STEP_LINK]: <https://www.codemag.com/Article/1907081/Nest.js-Step-by-Step>
   [NODE_JS_LINK]: <https://medium.com/zigbang/nodejs-event-loop%ED%8C%8C%ED%97%A4%EC%B9%98%EA%B8%B0-16e9290f2b30>
   [NODEVSSPRING_LINK]: <https://blog.naver.com/PostView.naver?blogId=biud436&logNo=222611201210&parentCategoryNo=&categoryNo=201&viewDate=&isShowPopularPosts=true&from=search>
   [ANYTHING_BLOG]: <https://any-ting.tistory.com/118?category=517156>
   [RYANSIN_BLOG]: <https://github.com/Ryan-Sin/swagger-nestjs-codegen>
