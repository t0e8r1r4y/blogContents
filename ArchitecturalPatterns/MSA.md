# MSA ( Micro Service Architecture )
- MSA란 마이크로 서비스 단위의 분산 아키텍처입니다.
- 제가 경험한 임베디드 시스템에서 분산 아키텍처 구성의 가장 큰 목적은 물리적인 SFOP로 시스템 중단을 방지하는 것이었습니다.
- 서비스 기업에서는 조직이나, 서비스 도메인 단위의 격리나 조직 분할 등의 목적을 용이하게 하는 목적도 있다고 들었습니다.

## 구성
- MSA 구성 내용은 [블로그][MSA_ARCH]에 정리하였습니다.
- 아래 내용은 MSA EZ 플랫폼에서 MSA에 대해서 학습한 내용을 정리하였습니다.
- 위 내용을 바탕으로 Notification Service를 MSA로 설계하고 구현하고자 합니다.


## MSA 학습을 진행한 플랫폼
| Title | Link |  
| ------ | ------ |  
| MSA EZ | [MSA 관련 학습][MSAEZ_LINK] |


## 플랫폼에서 사용한 툴
| Title | Link |  
| ------ | ------ |  
| MSA EZ | [MSA 관련 학습][MSAEZ_LINK] |
| Miro | |
| Xoom Designer | |

## 관련 도서 모음
| Title | 저자 혹은 링크 |  
| ------ | ------ |  
| Introducing Event Storming | Alberto Brandolini |
| DDD The First 15 Years | DDD Community |
| DDD Distilled | Vaughn Vernon |
| Learning DDD | Vlad Khononov |
| Patterns, Principles, and Practices of Domain-Driven Design | Scott Millett and Nick Tune |
| Overall MSA Design patterns: Microservices Patterns | |
| Database Design in MSA Lightly | [pdf](https://assets.confluent.io/m/2a60fabedb2dfbb1/original/20190307-EB-Making_Sense_of_Stream_Processing_Confluent.pdf) |
| Database Design in MSA Deep dive | Designing Data Intensive Applications |
| API design and REST | [링크](https://pepa.holla.cz/wp-content/uploads/2016/01/REST-in-Practice.pdf?fbclid=IwAR3XSyyeNpTqAehkNSesMyCv6Rnnuhqc901meKjsG6weWLab-u84xGiMJmw) |


[//]: # (These are reference links used in the body of this note and get stripped out when the markdown processor does its job. There is no need to format nicely because it shouldn't be seen. Thanks SO - http://stackoverflow.com/questions/4823468/store-comments-in-markdown-syntax)
   [MSAEZ_LINK]: <https://intro-kor.msaez.io/started/#%EC%A3%BC%EC%9A%94-features>
   [MSA_ARCH]: <https://medium.com/@tas.com/msa-micro-service-architecture-dfa4cc194f2a>
