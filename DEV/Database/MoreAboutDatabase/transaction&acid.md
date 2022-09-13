# Transaction과 Acid 내용 상세

# What is a database transaction?

- In short, a database transaction is a sequence of multiple operations performed on a database, and all served as a single logical unit of work — taking place wholly or not at all.
- In other words, there’s never a case that *only half of the operations* are performed and the results saved.
- When a database transaction is in flight, the database state may be temporarily inconsistent,
- but when the transaction is committed or ends, the changes are applied.

**Example**

To explain the concept of a database transaction, let us use a typical example of transferring money between Account A and Account B. Let’s say you want to move 5 dollars from Account A to Account B. This action can be broken down into the following simple operations:

1. Create a record to transfer 5 dollars from Account A to Account B. This is typically called the *begin* of a database transaction.
2. Read the balance from Account A.
3. Subtract 5 dollars from the balance of Account A.
4. Read the balance from Account B.
5. Add 5 dollars credit to Account B.

Now, if your database is running this transaction as one whole atomic unit, and the system fails due to a power outage, the transaction can be undone, reverting your database to its original state. Typically, a term like *rollback* refers to the process that undoes any changes made by the transaction, and the term *commit* is used to refer to a permanent change made by the transaction.

# **How do database transactions work?**

Before we learn about how database transactions work, let’s explore why they are needed in the first place.

1. System failures are inevitable, and in these cases, a transaction provides a way to ensure that the outcome is reliable and consistent. This means that the state of the database reflects all transactional changes committed before the point of failure and that transactions that were in-flight at the failure point are cleanly rolled back.
2. When multiple concurrent requests are hitting the database server, changing the same underlying data simultaneously, the transaction must isolate requests from each other to avoid conflicts.

![https://images.contentful.com/po4qc9xpmpuh/6jbcyfzdVJlc6XCUbzgMzb/96b1a9f0594f1d769f2254bd1abf25c1/database-transaction-1__1_.png](https://images.contentful.com/po4qc9xpmpuh/6jbcyfzdVJlc6XCUbzgMzb/96b1a9f0594f1d769f2254bd1abf25c1/database-transaction-1__1_.png)

During its lifecycle, a database transaction goes through multiple states. 

These states are called **transaction states** and are typically one of the following:

![https://images.contentful.com/po4qc9xpmpuh/3CQA2Vahq9s71Iifwz8SHG/15acd162da3b04a09d5c048aa121ce8d/database-transaction-2.png](https://images.contentful.com/po4qc9xpmpuh/3CQA2Vahq9s71Iifwz8SHG/15acd162da3b04a09d5c048aa121ce8d/database-transaction-2.png)

1. **Active states:** It is the first state during the execution of a transaction. A transaction is *active* as long as its instructions (read or write operations) are performed. → **트랜잭션의 연산들이 정상적으로 실행 중인 상태**
2. **Partially committed:** A change has been executed in this state, but the database has not yet committed the change on disk. In this state, data is stored in the memory buffer, and the buffer is not yet written to disk. → **트랜잭션 연산이 실행 된 상태이지만, 디스크가 아닌 메모리 버퍼에 임시 저장 된 상태**
3. **Committed:** In this state, all the transaction updates are permanently stored in the database. Therefore, it is not possible to rollback the transaction after this point. → **DB에 영구적으로 업데이트가 된 상태**
4. **Failed:** If a transaction fails or has been aborted in the active state or partially committed state, it enters into a *failed* state. → **트랜잭션이 중단 된 상태**
5. **Terminated state:** This is the last and final transaction state after a committed or aborted state. This marks the end of the database transaction life cycle. → **종료 된 상태**
6. **Abort** : **트랜잭션이 비정상적으로 종료되어 Rollback 연산을 수행한 상태**

# **What are ACID properties, and why are they important?**

# **Atomicity (원자성)**

**Atomicity in terms of a transaction means *all or nothing***. When a transaction is committed, the database either completes the transaction successfully or rolls it back so that the database returns to its original state. 

For example, in an online ticketing application, a booking may consist of two separate actions that form a transaction — reserving the seat for the customer and paying for the seat. 

A transaction guarantees that when a booking is completed, both these actions, although independent, happen within the same transaction. If any of the actions fail, the entire transaction is rolled back, and the booking is freed up for another transaction attempting to take it.

모든 작업이 반영되거나, 모두 롤백되는 특성.

수행중인 트랜잭션에 의해 변경된 내용은 ‘롤백 세그먼트’에 저장, 오류가 발생하는 경우 ‘롤백 세그먼트’에 저장된 정보로 롤백하여 원자성을 보장.

# **Consistency**

One of the key advantages of using a transaction is maintaining data integrity, regardless of whether it succeeds or fails. Transactions can only alter affected data in a way that is authorized by the database engine, ensuring that a consistent view of the data is maintained at all times. 

For example, when users deposit money in an online banking app, they want to see the result of this deposit reflected immediately when they view their balance. To ensure their money has not been lost. With strong transactional consistency, there should never appear to be more or less money in aggregate in the bank than there is.

트랜잭션 수행 전, 후에 데이터 모델의 모든 제약 조건을 만족하는 것을 보장

---

# **Isolation**

With multiple concurrent transactions running at the same time, each transaction should be kept independent without affecting other transactions executing simultaneously. 

For most database systems, the order of the transactions is not known in advance. Transactions are instead run in parallel, and some form of database locking is utilized to ensure that the result of one transaction does not impact that of another. 

Typically, databases offer several **[isolation levels](https://docs.fauna.com/fauna/current/concepts/isolation_levels)** to control the degree of transactional integrity.

하나의 자원에 대해서 병행 처리가 이루어 지기에, **lock & excute  unlock**을 통해 고립성을 보장

2PL 프로토콜을 사용하여 데드락을 방지함. → 여러 트랜잭션이 공유하고 있는 데이터에 동시에 접근할 수 없도록 하기위한 목적을 가진 프로토콜. Lock이 수행된 후에 Unlock이 수행되어야 한다는 것.

데이터 베이스마다 **격리수준이 정해져 있음.**

---

# **Durability**

Durability means that a successful transaction commit will survive permanently. To accomplish this, an entry is added to the database transaction log for each successful transaction.

한번 커밋 된 내용은 영구 적용 됨
