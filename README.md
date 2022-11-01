# 로드맵 따라서 기술 스택에 대한 `맥락정보`를 정리합니다.

# Career Road - DevOps & BackEnd


## 1. DevOps

### 1-1. Learn a Programming Language

- C : [C 프로그래밍 참고 Repo][C_LINK]
- C++, Go, Rust, Python, Ruby, [JS][JS_LINK]/[Node.js][NODEJS_LINK]

### 1-2. Understand different OS Concepts

- [POSIX][POSIX_LINK]
- [Networking][NETWORK_LINK]
- [Sockets][SOCK_LINK]
- [Procss][PROCANDTREAD_LINK]
- I/O Management
- Virtualization
- Memory / Storage
- [File System][FILE_LINK]
- Startup Managemet( initd )
- [Service Management ( systemd )][Systemd_Link]
- [Thread][PROCANDTREAD_LINK] and [Concurrency][CONCURRENCY_LINK]

### 1-3. Learn about Managing Servers

- [arm linux][ARM_LINUX_LINK]
- [linux command][COMMAND_LINK]
- [system monitoring][SYSMONITOR_LINK]
    
    

### 1-4. Networking, Security and Protocol

- FTP,  [SSH][SSH_LINK]
- [HTTP(HTTPS)][HTTP_LINK], SSL, TLS, Port Forwarding

### 1-5. What is and how to setup a _______?

- Proxy
    - Reverse Proxy
    - Forward Proxy
    - Firewall
    - Caching Server
    - Load Balancer
    - Web Server
        - Nginx, Tomcat
        - Caddy, Apache, IIS

<aside>
👇🏽 위 내용을 베이스로 실제 업무에서 사용되는 구현체에 대한 기술 스택들이 아래 내용이 됨

</aside>

---

### 1-6. Learn Infrastructure as Code

- [container][CONTAINER_LINK] : Docker, LXC
- Service Mesh : Consul, Istio, Envoy, Linkerd
- Configuration Mgmt : Ansible, Chef, Salt, Puppet
- Container Orchestration : Kubernetes, Docker Swarm, Nomad, Mesos
- Infrastructure Provisioning : Terraform, AWS CDK, CloudFormation, Pulumi

### 1-7. Learn som CI/CD Tool

- Jenkins, GitHub Actions, Travis CI
- Bamboo, TeamCity, Azure DevOps Service, Circle CI, Drone

### 1-8. Learn how to monitor software and infrastructure

- Infrastructure Monitoring : [Prometheus][PROMETHEUS_LINK], Grafana, Nagios, Zabbix, Monit, Datadog
- Application Monitoring : Jaeger, New Relic, AppDynamic, Istana, Open Telemety
- Logs Management : Elastic Stack, Graylog, Splunk, Papertail, Loki

### 1-9. Cloud Design Pattern

### 1-10. Cloud Providers

- AWS, Google Cloud, Alibaba, Digital Ocean
- Naver
- Azure, Linode, Heroku, Vultr

---

## 2. BackEnd

### 2-1. Internet

- [Web 동작 과정][WEBWORKING_LINK]
- DNS and how it works?
- hosting 이란?
- Browsers and how they work?

### 2-2. [Basic Frontend Knowlege][FRONT_LINK]

- HTML, CSS, JS
- React, tailwind

### 2-3. OS and General Knowledge

- [Terminal Usage][COMMAND_LINK]
- How OSs work in General
- Process Management
- Thread and concurrency
- Memory Management
- Interprocess Communication
- I/O Management
- POSIX Basics
- Basic Networking Concepts

### 2-4. Learn a Language + Framework

- [JAVA(Spring boot)][SPRING_LINK], [TS(NestJS)][TS_LINK]
- Rust, Go, C#, PHP, Python, Ruby, [JS][JS_LINK]

### 2-5. Version Control System & Repo hosting Service

- [Git & GitHub][GIT_LINK]

### 2-6. Database

- [데이터 베이스 스터디][DB_LINK]
- [Relational Database][RDB_LINK] : PostgreSQL, MySQL, MariaDB, MS SQL, Oracle
- [NoSQL Database][NoSQL_LINK] : Document, Column, Time series, Realtime
- [More about Database][MOREDB_LINK] : [ORMs][ORMs_LINK], [ACID & Transaction][TRANSCATIONACID_LINK], N+1 Problem, 데이터베이스 정규화/반정규화, [Indexes and how they work][INDEX_LINK]

### 2-7. APIs

- HATEOAS
- Open API Spec and Swagger
- Authntication
    - Cookie Based, [OAuth][OAuth_LINK], [JWT][JWT_LINK] etc…
- JSON APIs
- gRPC

### 2-8. [Caching][CACHE_LINL]

- CDN, Client Side, Server Side
- Redis, Memcached

### 2-9. Web Security Knowledge

- HTTPS, SSL/TLS, CORS, OWASP Security Risks, Content Security Policy
- Hashing Algorithms
    - scrypt, bcrypt, SHA Family
    

### 2-10. [Testing][TEST_LINK]

- Functional Testing → Unit Testing → Integration Testing

### 2-11. CI/CD

### 2-12. Design and Development Principles

- [Domain Driven Design][DDD_LINK]
- [Test Driven Development][TDD_LINK]
- [SOLID][SOLID_LINK]

### 2-13. Architectural Patterns

- Monolithic Apps
- [Microservices][MSA_LINK]
- SOA
- [CQRS][CQRS_LINK] and [Event Sourcing][EVENTSOURCING_LINK]
- [Serverless][SERVERLESS_LINK]
- [EDA][EDA_LINK]

### 2-14. Message Brokers

- Kafka
- RabbitMQ

### 2-15. Containerization vs Virtualization + Cloud

- [about Container][CONTAINER_LINK]
- docker

### 2-15. [GraphQL][GRAPHQL_LINK]

- [Apollo][APOLLO_LINK]
- Relay Modern

### 2-16. WebSockets



[//]: # (These are reference links used in the body of this note and get stripped out when the markdown processor does its job. There is no need to format nicely because it shouldn't be seen. Thanks SO - http://stackoverflow.com/questions/4823468/store-comments-in-markdown-syntax)
   [JS_LINK]: <https://github.com/t0e8r1r4y/blogContents/tree/main/DEV/lang/js/33-js-concepts>
   [C_LINK]: <https://github.com/t0e8r1r4y/C-CPLUS/blob/main/README.md>
   [NODEJS_LINK]: <https://jakearchibald.com/2015/tasks-microtasks-queues-and-schedules/>
   [TS_LINK]: <https://github.com/t0e8r1r4y/blogContents/tree/main/DEV/ts>
   [DB_LINK]: <https://github.com/t0e8r1r4y/blogContents/blob/main/DEV/Database/DatabaseStudy.md>
   [RDB_LINK]: <https://github.com/t0e8r1r4y/blogContents/blob/main/DEV/Database/RDB.md>
   [NoSQL_LINK]: <https://github.com/t0e8r1r4y/blogContents/blob/main/DEV/Database/NoSQL.md>
   [MOREDB_LINK]: <https://github.com/t0e8r1r4y/blogContents/blob/main/DEV/Database/MoreAboutDatabase.md>
   [TRANSCATIONACID_LINK]: <https://github.com/t0e8r1r4y/blogContents/blob/main/DEV/Database/MoreAboutDatabase/transaction%26acid.md>
   [ORMs_LINK]: <https://github.com/t0e8r1r4y/blogContents/blob/main/DEV/Database/MoreAboutDatabase/ORMs.md>
   [MSA_LINK]: <https://github.com/t0e8r1r4y/blogContents/blob/main/ArchitecturalPatterns/MSA.md>
   [EVENTSOURCING_LINK]: <https://github.com/t0e8r1r4y/blogContents/blob/main/ArchitecturalPatterns/EventSourcing.md>
   [CQRS_LINK]: <https://github.com/t0e8r1r4y/blogContents/blob/main/ArchitecturalPatterns/CQRS.md>
   [SERVERLESS_LINK]: <https://github.com/t0e8r1r4y/blogContents/blob/main/ArchitecturalPatterns/Serverless.md>
   [EDA_LINK]: <https://github.com/t0e8r1r4y/blogContents/blob/main/ArchitecturalPatterns/EDA.md>
   [INDEX_LINK]: <https://github.com/t0e8r1r4y/blogContents/blob/main/DEV/Database/Indexing.md>
   [APOLLO_LINK]: <https://github.com/t0e8r1r4y/blogContents/blob/main/GraphQL/Apollo.md>
   [TDD_LINK]: <https://github.com/t0e8r1r4y/blogContents/blob/main/DesignAndDevelopmentPrinciple/TDD.md>
   [DDD_LINK]: <https://github.com/t0e8r1r4y/blogContents/blob/main/DesignAndDevelopmentPrinciple/DDD.md>
   [SOLID_LINK]: <https://github.com/t0e8r1r4y/blogContents/blob/main/DesignAndDevelopmentPrinciple/SOLID.md>
   [CONTAINER_LINK]: <https://github.com/t0e8r1r4y/container-and-k8s/blob/main/README.md>
   [WEBWORKING_LINK]: <https://github.com/t0e8r1r4y/blogContents/blob/main/Internet/Web.md>
   [FRONT_LINK]: <https://github.com/t0e8r1r4y/blogContents/blob/main/BasicFront/BasicFront.md>
   [SPRING_LINK]: <https://github.com/t0e8r1r4y/springframewordk/blob/main/README.md>
   [CACHE_LINL]: <https://github.com/t0e8r1r4y/blogContents/blob/main/Cache/Cache.md>
   [GIT_LINK]: <https://github.com/t0e8r1r4y/blogContents/blob/main/GIT/git.md>
   [ARM_LINUX_LINK]: <https://github.com/t0e8r1r4y/blogContents/blob/main/linux/armlinux.md>
   [PROMETHEUS_LINK]: <https://github.com/t0e8r1r4y/blogContents/blob/main/monitorSoftwareAndInfrastructure/prometheus.md>
   [GRAPHQL_LINK]: <https://github.com/t0e8r1r4y/blogContents/blob/main/GraphQL/graphql.md>
   [TEST_LINK]: <https://github.com/t0e8r1r4y/blogContents/blob/main/testing/xUnit.md>
   [POSIX_LINK]: <https://github.com/t0e8r1r4y/blogContents/blob/main/OSConcepts/posix.md>
   [NETWORK_LINK]: <https://github.com/t0e8r1r4y/blogContents/blob/main/OSConcepts/Networking.md>
   [SOCK_LINK]: <https://github.com/t0e8r1r4y/blogContents/blob/main/OSConcepts/Sockets.md>
   [PROCANDTREAD_LINK]: <https://github.com/t0e8r1r4y/blogContents/blob/main/OSConcepts/ProcessAndThread.md>
   [FILE_LINK]:  <https://github.com/t0e8r1r4y/blogContents/blob/main/OSConcepts/FileSystem.md>
   [JWT_LINK]: <https://github.com/t0e8r1r4y/blogContents/blob/main/APIS/jwt.md> 
   [OAuth_LINK]: <https://github.com/t0e8r1r4y/blogContents/blob/main/APIS/OAuth.md>
   [Systemd_Link]: <https://github.com/t0e8r1r4y/blogContents/blob/main/linux/systemd.md>
   [SSH_LINK]: <https://medium.com/@tas.com/ssh-%ED%94%84%EB%A1%9C%ED%86%A0%EC%BD%9C-f4079b1103ab>
   [HTTP_LINK]: <https://medium.com/@tas.com/http-websocket-3dbf0ae22be9>
   [COMMAND_LINK]: <https://github.com/t0e8r1r4y/blogContents/blob/main/linux/command.md>
   [SYSMONITOR_LINK]: <https://github.com/t0e8r1r4y/blogContents/blob/main/linux/monitoring.md>
   [CONCURRENCY_LINK]: <https://github.com/t0e8r1r4y/blogContents/blob/main/OSConcepts/Concurrency.md>
