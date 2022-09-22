<h1 align="center">
  <br>
  <img src="https://nesoy.github.io/assets/logo/database.jpg"  width=600"></a>
  <br>
  <br>
  데이터베이스 잘하기 ( 스터디 그룹 주제 )
  <br>
  <br>
</h1>


## 소개

이 레포지토리는 데이터베이스 스터디 목적으로 개설하였습니다. 기본은 SQLP 내용을 바탕으로 RDB, NoSQL, 대용량 분산 데이터베이스 및 분산 데이터 처리 툴에 대해서 학습한 내용을 정리합니다. 데이터 베이스에 대한 이해도를 높이고, 자격증도 하나 따봅시다.

## 목차

1. **[메인 자료](#1-메인-자료)**
1. **[부 주제](#2-부-주제)**
1. **[NoSQL 분류](#3-NoSQL-분류)**



## 1. 메인 자료
| TITLE | LINK | SUMMERY | 
| ------ | ------ | ------ |
| 오라클 성능 고도화 원리와 해법 | | SQLP 메인 교재 |
| 친절한SQL튜닝 |[wiki][BOOK_WIKI] | 개발자를 위한 SQL 튜닝 입문서 |

## 2. 부 주제
| TITLE | LINK | SUMMERY | 
| ------ | ------ | ------ |
| MongoDB | [몽고 공식][MONGO] | document db |
| spark | [스파크 git][SPARK] | 빅데이터 분석 프레임워크 |
| hive | [하이브 깃][HIVE] | 하둡에서 동작하는 데이터 웨어하우스 인프라 구조로서 데이터 요약, 질의 및 분석 기능을 제공 |
| trino | [트리노 공식][TRINO] | 빅데이터를 쿼리하기 위한 분산 SQL 쿼리 엔진 |
| hadoop | [하둡 git][HADOOP] | 대용량 자료를 처리할 수 있는 큰 컴퓨터 클러스터에서 동작하는 분산 응용 프로그램을 지원하는 프레임워크|

                                                                         

- Snowflake, Velox, Bigquery 등 대용량 분산 데이터베이스 및 분산 데이터 처리 툴

                                                                         

## 3. NoSQL 분류
- [자료출처][NoSql]  
                                                                         
                                                                         
| TITLE | Product Name | who? | 
| ------ | ------ | ------ |
| Key-value-cache | Memcached | |
| Key-value-store | DynamoDB | |
| Key-value-store | Redis | |
| Tuple-store | River | |
| Document-store | MongoDB | |
| Wide-columnar-store | Hbase | |                                                                         
| Wide-columnar-store | Cassandra | |
| Time-series | InfluxDB | |
| Time-series | Druid | |
| Time-series | Pinot | |
                                                                         
---
**Thanks!**

[//]: # (These are reference links used in the body of this note and get stripped out when the markdown processor does its job. There is no need to format nicely because it shouldn't be seen. Thanks SO - http://stackoverflow.com/questions/4823468/store-comments-in-markdown-syntax)
   [NoSql]: <http://www.opennaru.com/jboss/nosql-is-a-horseless-carriage>
   [HIVE]: <https://github.com/apache/hive>
   [TRINO]: <https://trino.io/>
   [HADOOP]: <https://git-wip-us.apache.org/repos/asf?p=hadoop.git>
   [SPARK]: <https://github.com/apache/spark>
   [BOOK_WIKI]: <https://github.com/t0e8r1r4y/SQLP_STUDY/wiki>
   [MONGO]: <https://www.mongodb.com/>
