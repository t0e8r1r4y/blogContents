# 동시성 문제

> 여러 쓰레드가 동시에 같은 인스턴스의 필드 값에 접근하여 조작하는 행위로 인해 발생하는 문제를 의미

<br/>

## [Concurrency in C](https://www.classes.cs.uchicago.edu/archive/2018/spring/12300-1/lab6.html)
- c언어에서도 멀티쓰레딩을 사용하다보면 동시성 이슈가 생긴다.
- 해소 방법은 뮤텍스나 세마포어를 사용하거나
- [조건 변수를 통한 스레드 동기화](https://reakwon.tistory.com/99)를 할 수도 있음.
- 또한 EDP에서 컨슈머와 프로듀서간 동기화 또한 조건 변수를 사용하거나 아래 예시처럼 flag를 사용하여 처리가 가능합니다.
```C

void pushQueue(unsigned char* scrData, MESSAGEQUEQUE_T* queue )
{
    int queueIndex = 0;
    size_t i = 0;

    for (i = 0; i < MQSIZE; i++)
    {
        /* code */
        queueIndex = (( queue->queueWritePtr + i ) % MQSIZE );

        if( queue->q[queueIndex].used == FALSE) // 이벤트 큐에서 플래그를 처리한 부분
        {
            queue->q[queueIndex].used       = USED;
            queue->q[queueIndex].dataBuffer = (unsigned char*)malloc(strlen((const char *)scrData) +1 );

            memcpy(queue->q[queueIndex].dataBuffer, (unsigned char*)scrData, strlen((const char *)scrData) +1);

            queue->queueWritePtr            = queueIndex + 1;
            queue->q[queueIndex].used       = TRUE;
            break;
        }
    }

    if( i >= (MQSIZE-1) ) printf("Queue Overflow\r\n");
    
    return;
}
```

<br/>


## Concurrency in java

`WAS 와 멀티 쓰레드`에서 말했듯이, 싱글톤 객체는 조심히 사용해야한다고 했다. 어떤 부분을 조심해야할까?

바로, `상태 값이 유지되지 않게 설계`해야 한다는 것이다. 아래 코드를 보자.

```java
@Service
public class UserService {

    private UserId userId; // 상태 값

    public void createUser(User user) {
        // 여기서 userId 값을 변경하는 코드가 존재
    }
}
```

UserService 는 싱글톤 객체로 등록되는 빈이다. 위 코드에서 UserId 라는 객체가 상태 값인데, 회원 가입 100건이 동시에 이루어졌다고 하면 userId 라는 `상태값은 안전할까? 안전하지 않을까?` 이 부분에 대한 답을 명확하게 할 수 있다면 `프로세스와 쓰레드`에 대한 개념을 잘 이해하고 있다고 볼 수 있고, 답을 내리지 못한다면 프로세스와 쓰레드에 대한 개념을 다시 공부해야 할 것이다.

위로 올라가서 프로세스와 쓰레드를 다시 한 번 살펴보자.

쓰레드는 프로세스의 Stack, Heap, Data, Text 영역 중 Stack 부분을 제외한 나머지를 공유한다. 그리고 userId 의 상태 값은 전역변수이며 Process 의 Data 영역에 적재된다. 즉, 우리가 개발하는 멀티 쓰레드 환경에서 수 많은 쓰레드들이 userId 라는 상태 값(전역 변수)을 공유하게 되는 것이다. 그렇게되면, 회원 가입후에 서로 다른 사람의 개인정보가 보인다는 등, 심각한 오류가 발생한다.

따라서, 위와 같은 코드는 절대 짜면 안된다. 비록 트래픽이 낮은 애플리케이션일지라도 말이다.

그러면 동시성 이슈를 피하기 위해서 어떻게 해야할까? 이것에 대한 해답도 역시 `프로세스와 쓰레드`에 있다. 쓰레드의 Stack 영역은 공유하지 않으며, 지역 변수가 저장된다. 따라서, 전역 변수대신 지역 변수를 쓰게끔 하면 적은 노력으로 동시성 문제를 피할 수 있다.

동시성 문제가 발생하는 곳은 같은 인스턴스의 필드(주로 싱글톤에서 자주 발생), 또는 static 같은 공용 필드에 접근할 때 발생한다. 동시성 문제는 값을 읽기만 하는 경우에는 발생하지 않고, 어디선가 값을 변경하기 때문에 발생하는 문제이다.

그런데, 싱글톤 객체에서 상태 값을 가져야하는 경우가 있을 수 있는데, 이때는 어떻게 동시성 이슈를 피할까? 

## ThreadLocal

싱글톤 빈에서 상태값을 유지해야하는 경우에 동시성 이슈를 해결하기 위해서 `ThreadLocal`을 지원한다. 

ThreadLocal 은 해당 쓰레드만 접근할 수 있는 특별한 저장소(별도의 내부 저장소를 제공)를 의미한다. 따라서, 여러 쓰레드가 동시에 상태 값에 접근해도 동시성 이슈가 발생하지 않는다.

위 코드에 ThreadLocal 을 적용해보자.

```java
@Service
public class UserService {

    private ThreadLocal<UserId> userIdStore = new ThreadLocal<>(); 

    public void createUser(User user) {
        userIdStore.set(user.createUserId());
        UserId userId = userIdStore.get();
    }
}
```

위 처럼 ThreadLocal 을 적용하여 사용하면, 각 쓰레드는 UserId 를 가져오기 위해 자신만의 별도의 내부 저장소에서 꺼내기 때문에 동시성 이슈로부터 안전하다.

### ThreadLocal 사용 시 주의할 점

ThreadLocal 을 사용할 때의 주의점은 해당 쓰레드가 쓰레드 로컬을 모두 사용하고 나면 `ThreadLocal.remove()` 를 호출해서 쓰레드 로컬에 저장된 값을 제거해주어야 한다. 제거하지 않으면 특정 상황에서 메모리 누수, 개인정보 등의 문제가 발생할 수 있다.

ThreadLocal 의 값을 사용 후 제거하지 않고 그냥 두면 WAS 처럼 쓰레드 풀을 사용하는 경우에 심각한 문제가 발생할 수 있다.

쓰레드 풀은 요청 마다 쓰레드를 생성했을 경우의 단점을 보완하기 위해 만들어졌다고 위에서 배웠다. 따라서, WAS 는 쓰레드 사용이 끝나면 해당 쓰레드를 다시 반납한다.

A 사용자가 회원 가입 요청을 하여 `thread-A` 가 할당되었다. thread-A 가 사용자의 A 의 데이터(User)를 자신의 전용 보관소인 `thread-A-privacy-storage` 에 저장한다.

A 의 요청이 끝나고나면 WAS 는 사용이 끝난 thread-A 를 재사용하기 위해서 쓰레드 풀에 반환한다.
따라서, thread-A 가 제거되지 않았으므로 thread-A-privacy-storage 도 살아있게된다.

B 사용자가 자신의 정보를 조회하기 위한 요청을 한다. WAS 는 쓰레드 풀에서 남는 쓰레드를 할당해주는데, 이때 어떤 쓰레드가 할당될지는 모른다. thread-A 가 할당될 수도 있고, 다른 쓰레드가 할당될 수 도 있다. thread-A 가 할당되면 thread-A-privacy-storage 에 들어있던 사용자 A 에 대한 개인정보가 조회된다. 따라서, 다른 사람의 개인정보가노출 되는 심각한 문제가 발생할 수 있다.

그렇게 때문에 ThreadLocal 을 사용하고 나서 `ThreadLocal.remove()` 를 통해 자신의 전용 보관소에 저장되어 있던 값들을 모두 제거해주어야 한다.

## Thread Safe 하게 설계하는 방법

Thread Safe 란 쉽게 말하면 동시성 이슈가 발생하지 않도록 설계하는 것을 말하고, OS 지식과 섞어서 풀어 설명하면, 쓰레드가 경쟁 상태(race condition)일 때 임계 구역에 있는 공유 변수의 일관성을 유지시키도록 설계하는 것을 말한다.

- java.util.concurrent 패키지 하위의 클래스사용하기
    - Ex. ConcurrentHashMap 등
- 인스턴스 변수를 두지 않습니다. = 상태 값 두지 않기
- Singleton 패턴을 사용
    - 일반적으로 구현하는 Singleton Pattern 은 Thread-safe 하지 않는다.
    - 인스턴스가 1개만 생성되는 특징을 가진 싱글턴 패턴을 이용하면, 하나의 인스턴스를 메모리에 등록해서 여러 스레드가 동시에 해당 인스턴스를 공유하여 사용하게끔 할 수 있으므로, 요청이 많은 곳에서 사용하면 효율을 높일 수 있다.
    - 보통은 `LazyHolder` 방식을 주로 사용한다.
        - JVM 의 Class loader 매커니즘을 이용한 방법
- 동기화 블럭(synchronized) 지정
