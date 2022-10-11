# MSA ( Micro Service Architecture )
- MSA란 마이크로 서비스 단위의 분산 아키텍처입니다.
- 제가 경험한 임베디드 시스템에서 분산 아키텍처 구성의 가장 큰 목적은 물리적인 SFOP로 시스템 중단을 방지하는 것이었습니다.
- 서비스 기업에서는 조직이나, 서비스 도메인 단위의 격리나 조직 분할 등의 목적을 용이하게 하는 목적도 있다고 들었습니다.

## 구성
- MSA를 ebay 비즈니스 모델에 적용시켜 `설계`한 내용과 MSA 구성은 [블로그][MSA_ARCH]에 정리하였습니다.
- 아래 내용은 MSA EZ 플랫폼에서 MSA에 대해서 학습한 내용을 정리하였습니다.
- 위 내용을 바탕으로 Notification Service를 MSA로 설계하고 구현하고자 합니다.


<br/>

## 학습 구성

#### Biz
- 비즈니스를 분석하고 설계하는 단계입니다.
- 학습 사이트의 설계 도구가 필요합니다.
- 이벤트 스토밍을 통해 필요한 구성요소를 작성하고 이를 구현합니다.


#### Dev
| No | Title | Link |
| ------ | ------ | ------ |
| 1 | 게이트웨이를 통한 진입점 통일 | |
| 2 | Req/Res 방식의 MSA 연동 | |
| 3 | Req/Res 방식에 장애 전파 차단(`서킷브레이커` 사용) | |
| 4 | JWT 토큰 기반 인증인가 w/ Keycloak Authz-svr | [{구현} Spring JWT 사용][JWT-SPRING] |
| 5 | Authz 서버 설정 w/ GUI Console | |
| 6 | Gateway에 OAuth2 Client 설정 | [ (구현)Google OAuth 사용][Google-OAuth] |
| 7 | 주문서비스에 Fine grained RBAC 설정 | |
| 8 | Pub/Sub 방식의 MSA 연동 | |
| 9 | Pub/Sub - Compensation and Correlation | |
| 10 | Kafka 스케일링 | |
| 11 | Kafka 수동커밋 | |
| 12 | Retry & Dead Letter Queue | |
| 13 | Data Pipeline w/ Kafka Connect | |
| 14 | 데이터프로젝션-컴포지트서비스 | |
| 15 | 데이터프로젝션-GraphQL | |
| 16 | CQRS 샘플 모델링 | |
| 17 | Docker Image Build & Push| |
| 18 | Pub/Sub 방식의 MSA 연동 | |



#### Ops
- 개인 프로젝트에서 Ops에 대한 관리가 AWS를 사용하는 것이 더 편리하기에 아래 내용은 '설치하고 써봤다.' 정도로 마무리했습니다.
- 별도의 dev ops팀이 있고 규모가 크지 않는한, 아마도 제 생각에는 아래 환경을 다 갖추고 운영해보기는 어렵지 않을까 싶고, AWS가 편리한 부분이 많은 듯합니다.


| No | Title | Link |
| ------ | ------ | ------ |
| 1 | Docker Basics | |
| 2 | AWS Cloud, k8s Cluster 환경설정 | |
| 3 | 컨테이너 생성 무작정 따라하기 | |
| 4 | 객체 식별자와 Annotations | |
| 5 | 12번가 마이크로서비스 배포 | |
| 6 | Microservices 자동확장 (Auto Scaling) | |
| 7 | Pod & 마이크로서비스 트러블 슈팅 | |
| 8 | Namespaces를 활용한 Cluster 가상화 | |
| 9 | Kubernetes 로더 밸런서-Service | |
| 10 | Cloud 저장소 Persistent Volume(AWS) | |
| 11 | 환경설정 관리- ConfigMap/Secret | |
| 12 | Self-healing & Zero-downtime Deploy | |
| 13 | k8s L7 Router - Ingress | |
| 14 | 12번가 Mall에 토큰인증 적용하기 | |
| 15 | Mircoservice 모니터링 w/ Prometheus&Grafana | [프로메테우스 사용경험][Spring-prometheus] |
| 16 | MSA Logging with EFK Stacks | |
| 17 | 컨테이너 운영 무작정 따라하기 | |
| 18 | Service Mesh; Istio | |
| 19 | Service Mesh: Traffic Mgmt & Canary 배포 | |
| 20 | Service Mesh: Timeout & Retry | |
| 21 | Service Mesh: Circuit Breaker | |
| 22 | Service Mesh: Istio Metrics based HPA | |
| 23 | Service Mesh: MSA 모니터링 w/ Istio addon Grafana | |
| 24 | Kubernetes Utilities | |

## MSA 학습을 진행한 플랫폼
| Title | Link |  
| ------ | ------ |  
| MSA EZ | [MSA 관련 학습][MSAEZ_LINK] |


## 참고자료
#### 플랫폼에서 사용한 도구
| Title | Link |  
| ------ | ------ |  
| MSA EZ | [MSA 관련 학습][MSAEZ_LINK] |
| Miro | |
| Xoom Designer | |

#### 관련 도서 모음
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

#### SNS
| Title | Link |  
| ------ | ------ | 
| DDD Facebook | [링크][DDD Facebook] |

[//]: # (These are reference links used in the body of this note and get stripped out when the markdown processor does its job. There is no need to format nicely because it shouldn't be seen. Thanks SO - http://stackoverflow.com/questions/4823468/store-comments-in-markdown-syntax)
   [MSAEZ_LINK]: <https://intro-kor.msaez.io/started/#%EC%A3%BC%EC%9A%94-features>
   [MSA_ARCH]: <https://medium.com/@tas.com/msa-micro-service-architecture-dfa4cc194f2a>
   [DDD Facebook]: <https://www.facebook.com/groups/cloudswmoding>
   [Spring-prometheus]: <https://github.com/t0e8r1r4y/springframewordk/blob/main/prometheus_spring/README.md>
   [JWT-SPRING]: <https://github.com/t0e8r1r4y/springframewordk/blob/main/jwt/springjwt.md>
   [Google-OAuth]: <https://github.com/t0e8r1r4y/springframewordk/tree/main/googleAuth>
