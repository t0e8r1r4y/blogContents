# 캐시와 관련된 내용을 정리함

- 캐시의 정의는 데이터나 값을미리 복사해 놓는 임시 장소(메모리에 할당 된 저장공간)
- 일정한 저장공간을 메모리에 할당하여 빠른 읽기 성능이 요구되는 데이터를 임시저장하고 해당 위치에서 읽어 조회 성능을 높이기 위한 목적으로 사용하는 기술입니다.

## 캐시 사용전략
- [redis 캐시전략][CACHE_STRATEGY]

## OS에서 사용하는 캐시
- [페이지 캐시와 버퍼캐시][MYBLOG_LINK]

## DB에서 사용하는 캐시
- [oracle database의 구조][ORACLE_STUDY_LINK]

## 웹 백엔드 성능 최적화에서 사용하는 캐시
-  [spring local cache][SPINRG_LOCAL_CACHE]
-  [redis 캐시전략][MY_BLOG2_LINK]

## 프론트엔드 웹 성능 개선에 사용되는 캐시
| 종류 | 위치 | 설명 |
| --- | --- | --- |
| 브라우저 캐시 | 브라우저 | 한 번 받아온 리소스들을 재사용하여 속도가 빨라짐 |
| 프록시 캐시 | 브라우저와 ISP | 조직 내에서 접속하는 웹 사이트의 리소스들을 캐시하여 속도가 빨라지고 네트워크 사용량을 줄임 |
| 트랜스페어런트 캐시 | ISP | ISP는 이 캐시를 이용하여 ISP간 대역폭 낭비를 줄임 |
| 리버스 프록시 캐시 | ISP와 웹 서버 | 원본 서버로의 트래픽을 줄이고, 사용자에게 빠른 응답을 준다. |
| 웹 캐시 | 웹 서버와 브라우저 중간에 위치 | 원본 콘텐츠 요청을 서버로부터 받은 후 복사본을 만들어 저장하고 클라이언트에 응답 |



[//]: # (These are reference links used in the body of this note and get stripped out when the markdown processor does its job. There is no need to format nicely because it shouldn't be seen. Thanks SO - http://stackoverflow.com/questions/4823468/store-comments-in-markdown-syntax)
   [MYBLOG_LINK]: <https://medium.com/@tas.com/%ED%8C%8C%EC%9D%BC-%EC%8B%9C%EC%8A%A4%ED%85%9C%EC%97%90-%EB%8C%80%ED%95%9C-%EA%B8%B0%EC%B4%88%EC%A0%81%EC%9D%B8-%EA%B0%9C%EB%85%90%EC%A0%95%EB%A6%AC-9144dabce95d>
   [ORACLE_STUDY_LINK]: <https://github.com/kmw8551/study/blob/main/oraclearch/src/main/java/oracle/20220925_1%EC%9E%A5.md>
   [CACHE_STRATEGY]: <https://medium.com/@tas.com/%EC%BA%90%EC%8B%9C-cache-%EC%99%80-cache%EC%A0%84%EB%9E%B5-6cde62a2c9d8>
   [MY_BLOG2_LINK]: <https://medium.com/@tas.com/cache-aside-%ED%8C%A8%ED%84%B4-%EA%B5%AC%ED%98%84%EC%9D%84-%ED%86%B5%ED%95%9C-springboot-redis-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0-6416039b96a5>
   [SPINRG_LOCAL_CACHE]: <https://wave1994.tistory.com/182>
