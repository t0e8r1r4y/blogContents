# More about Database

## 목차

1. **[ACID & Transactions](#1-acid-transactions)**
1. **[ORMs](#2-orms)**
1. **[N+1 Problem](#3-'n+1'-problem)**
1. **[Data Replication](#4-data-replication)**
1. **[Sharding Strategies](#5-sharding-strategies)**
1. **[CAP Theorem](#6-cap-theorem)**

## 1. ACID Transactions


- [세부내용][ACIDTRANSACTION_LINK]
- Transcation 요약
    - a database transaction is a sequence of multiple operations performed on a database, and all served as a **single logical unit of work** — taking place wholly or not at all. In other words, there’s never a case that *only half of the operations* are performed and the results saved. When a database transaction is in flight, the database state may be temporarily inconsistent, but when the transaction is committed or ends, the changes are applied.
    - 여러 작업을 하나로 묶은 작업수행의 논리적 단위.
    - 사용 목적 : 병렬 처리 과정에서 **데이터 부정합을 방지**하고자 할 때 사용. 따라서 트랜잭션에서 중요한 것은 데드락 방지를 위한 스케쥴링.
    - 트랜잭션 라이프 사이클
        
- ACID 요약
    - Atomicity
        - 트랜잭션의 작업은 All or Nothing의 개념으로 부분적으로 실행되거나 중단되지 않음을 보장함
    - Consistency
        - 트랜잭션이 성공적으로 완료되면 일괄적인 DB상태를 유지하는 것
    - Isolation
        - 트랜잭션 수행 시 다른 트랜잭션의 작업이 끼어들지 못하도록 보장
    - Durability
        - commit을 하면 현재 상태는 영원히 보장됨.

---

## 2. ORMs

## 3. N+1 Problem

## 4. Data Replication

## 5. Sharding Strategies

## 6. CAP Theorem



**Thanks!**

[//]: # (These are reference links used in the body of this note and get stripped out when the markdown processor does its job. There is no need to format nicely because it shouldn't be seen. Thanks SO - http://stackoverflow.com/questions/4823468/store-comments-in-markdown-syntax)
   [ACIDTRANSACTION_LINK]: <https://github.com/t0e8r1r4y/blogContents/blob/main/DEV/Database/MoreAboutDatabase/transaction%26acid.md>
