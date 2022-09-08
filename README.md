# 로드맵 따라서 기술 스택 정리하기

# Career Road - DevOps & BackEnd

<aside>
  [바로가기] 키워드(링크)
</aside>

## 1. DevOps

### 1-1. Learn a Programming Language

- C
- C++, Go, Rust, Python, Ruby, [JS][JS_LINK]/Node.js

### 1-2. Understand different OS Concepts

- POSIX
- Networking
- Sockets
- Procss
- I/O Management
- Virtualization
- Memory / Storage
- File System
- Startup Managemet( initd )
- Service Management ( systemd )
- Thread and Concurrency

### 1-3. Learn about Managing Servers

- arm linux
- linux command
    - ps, top, htop, atop, lsof, nmon, iostat, sar, vmstat, mtr, ping, nmap, netstat, strace, ftrace, du, df, dmesg, exec, fork, uname -ar,
    - awk, sed, grep, egrep, echo, chmod
- system monitoring
    
    

### 1-4. Networking, Security and Protocol

- FTP,  SSH
- HTTP(HTTPS), SSL, TLS, Port Forwarding

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

- container : Docker, LXC
- Service Mesh : Consul, Istio, Envoy, Linkerd
- Configuration Mgmt : Ansible, Chef, Salt, Puppet
- Container Orchestration : Kubernetes, Docker Swarm, Nomad, Mesos
- Infrastructure Provisioning : Terraform, AWS CDK, CloudFormation, Pulumi

### 1-7. Learn som CI/CD Tool

- Jenkins, GitHub Actions, Travis CI
- Bamboo, TeamCity, Azure DevOps Service, Circle CI, Drone

### 1-8. Learn how to monitor software and infrastructure

- Infrastructure Monitoring : Prometheus, Grafana, Nagios, Zabbix, Monit, Datadog
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

- Web 동작 과정
- DNS and how it works?
- hosting 이란?
- Browsers and how they work?

### 2-2. Basic Frontend Knowlege

- HTML, CSS, JS
- React, tailwind

### 2-3. OS and General Knowledge

- Terminal Usage
- How OSs work in General
- Process Management
- Thread and concurrency
- Memory Management
- Interprocess Communication
- I/O Management
- POSIX Basics
- Basic Networking Concepts

### 2-4. Learn a Language + Framework

- JAVA(Spring boot), TS(NestJS)
- Rust, Go, C#, PHP, Python, Ruby, [JS][JS_LINK]

### 2-5. Version Control System & Repo hosting Service

- Git & GitHub

<aside>
👇🏽 현재 조금 집중이 필요한 부분!!

</aside>

### 2-6. Database

- Relational : PostgreSQL, MySQL, MariaDB, MS SQL, Oracle
- ORMs, ACID, Transaction, N+1 Problem, 데이터베이스 정규화/반정규화 Indexex and how they work

### 2-7. APIs

- HATEOAS
- Open API Spec and Swagger
- Authntication
    - Cookie Based, OAuth, JWT etc…
- JSON APIs
- gRPC

### 2-8. Caching

- CDN, Client Side, Server Side
- Redis, Memcached

### 2-9. Web Security Knowledge

- HTTPS, SSL/TLS, CORS, OWASP Security Risks, Content Security Policy
- Hashing Algorithms
    - scrypt, bcrypt, SHA Family
    

### 2-10. Testing

- Functional Testing → Unit Testing → Integration Testing

### 2-11. CI/CD

### 2-12. Design and Development Principles

- Domain Driven Design
- Test Driven Development
- SOLID

### 2-13. Architectural Patterns

- Monolithic Apps
- Microservices
- SOA
- CQRS and Event Sourcing
- Serverless

### 2-14. Message Brokers

- Kafka
- RabbitMQ

### 2-15. Containerization vs Virtualization + Cloud

- docker

### 2-15. GraphQL

- Apollo
- Relay Modern

### 2-16. WebSockets



[//]: # (These are reference links used in the body of this note and get stripped out when the markdown processor does its job. There is no need to format nicely because it shouldn't be seen. Thanks SO - http://stackoverflow.com/questions/4823468/store-comments-in-markdown-syntax)
   [JS_LINK]: <https://github.com/t0e8r1r4y/blogContents/tree/main/DEV/lang/js/33-js-concepts>
