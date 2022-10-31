# 프로세스와 쓰레드

> 정리 원문은 [medium 블로그](https://medium.com/@tas.com/process-thread-%EC%83%9D%EC%84%B1%EA%B3%BC-%EC%A2%85%EB%A3%8C-ff31cdde2b40)에 작성하였습니다. 

## 용어 정의

- Program : 파일이 저장 장치에 저장되어 있지만 메모리에는 올라가 있지 않는 정적인(static) 상태.
- Process : program이 실행되어 메모리에 적재 되고(vms+pcb), 실행을 대기하거나 실행하는 실행 흐름.
- Thread : 프로세스 코드에 정의 된 절차에 따라 실행 되는 특정한 수행 경로.


<br/>


## Thread가 필요한 이유

OS가 없는 펌웨어의 경우 실행 시작부터 실행 종료까지 프로세스 하나에서 모든 처리 동작을 진행함. ( 이 경우 특정 처리에 실행 시간이 많아지지 않도록 하기 위해서, 각 처리당 처리시간을 분배하여 개발자가 정의 해야 함 )

하지만 처리 동작의 복잡성이 증가함에 따라 각 처리 동작을 여러 프로세스를 사용하게 되면 아래의 문제가 생긴다.

여러가지 처리 동작에 따라서 상호 프로세스간 통신을 위해 IPC가 필요함.
각 프로세스가 메모리 영역을 독립적으로 사용하기 때문에, 처리 동작의 순서, 처리 방법에 따라 컨텍스트 스위칭에 대한 비용이 발생함.
그리고 프로그램 설계자가 제대로 설계하지 못하면, 각각의 처리동작이 꼬이면서 원하는 목적 달성이 안될 수 있음

<br/>


## Thread

![다운로드](https://user-images.githubusercontent.com/91730236/198837901-1fa16052-7d5f-41f9-be7f-8cb1a8e57893.png)

Thread는 하나의 프로그램 내에 존재하는 여러 개의 실행 흐름을 위한 특정한 수행 경로이다. 위 이미지에서 보듯 메모리 영역을 공유하기 때문에 컨텍스트 스위칭에서 발생하는 오버헤드가 줄어들고, 프로세스간 IPC 통신에 비해 통신이 간단함.

<br/>

## Process와 Thread의 관계
- Process는 하나이상의 Thread를 포함한다.
- Thread가 없는 Process는 존재하지 않는다.



## Process
- Program이 실행되어 메모리에 적재 되고, 실행을 대기하거나 실행하는 실행 흐름.
- 위 정의에 따르면 process의 정보는 2가지가 필요하다. ( task_struct, process stack, thread_info )

  - task_struct : process가 쓰는 메모리 리소스, 프로세스 이름, 실행 시각, 프로세스 아이디, 프로세스 스택의 최상단 주소와 같은 속성 정보가 저장 됨
  - process stack 공간 : 실행 흐름을 표현하는 공간, process stack의 최상단 주소에 thread_info 구조체가 있음.
  - task_struct 구조체 : 태스트 디스크립터
  - thread_info 구조체 : 프로세스 스레드 정보


<br/>



## 프로세스는 어떻게 생성이 되는가?
- process는 program 실행 명령을 내리면 프로세스 생성을 전담하는 프로세스가 있음. ps 명령 입력시 1번과 2번에 할당 된 init과 kthreadd라는 프로세스임

  - init process : user mode에서 프로세스 생성 요청이 있을 경우 생성하는 프로세스 ( sys_clone() 시스템 콜 핸들러 함수 호출 )
  - kthreadd process : 커널 레벨 프포세스 생성 요청이 있을 경우 생성하는 프로세스 ( kernel_thread() 함수 호출 )
  - process는 생성 요청이 있는 그 타이밍에 매번 생성을 하는 것이아닌, 미리 메모리를 할당 해두고 생성 요청이 있을 때 미리 생성해둔 것들을 사용 함. Slub Memory Allocator(커널 메모리 할당자)가 미리 메모리를 할당 해둠. 이를 통해 리소스 할당에 소요되는 시간을 단축함
  - 그리고 프로세스 생성과정에서 매번 새로운 프로세스 자료구조를 생성하는 것이 아닌, 부모 프로세스의 자료구조를 복사해서 거기에 할당해서 사용함.



<br/>



## init process가 process를 생성하는 과정

    fork()
    sys_clone()
    _do_fork()
    copy_process()

<br/>


## kthreadd process가 process를 생성하는 과정

    kthread_create
    kthread_create_on_node
    __kthread_create_on_node
    scheduling
    kthread
    created_kthread
    kernel_thread
    _do_fork()
    _do_fork() 함수의 동작

<br/>

## 프로세스 생성
- 생성한 프로세스의 실행 요청
- copy_process() 함수를 호출하여 부모프로세스의 리소스를 자식 프로세스에 복제. 그리고 wake_up_new_task() 함수를 호출해서 스케줄러에게 프로세스 실행 요청을 하는 행위를 함.

## 프로세스의 종료

- 프로세스는 do_exit()함수를 사용해서 종료를 함.
- user process에서는 exit() 함수를 사용하여 sys_exit_group() -> do_group_exit() -> do_exit() 순으로 진행하여 종료
- kernel process에서는 kill 명령어를 사용하여 slow_work_pending() -> do_work_pending() -> do_signal() -> do_group_exit() -> do_exit() 순으로 진행하여 종료
- do_exit() 함수의 동작 방식 확인

      init process가 종료하면 강제 커널 패닉 유발: 보통 부팅 과정에서 발생함
      이미 프로세스가 do_exit() 함수의 실행으로 프로세스가 종료되는 도중 다시 do_exit() 함수가 호출되었는지 점검
      프로세스 리소스(파일 디스크립터, 가상 메모리, 시그널) 등을 해제
      부모 프로세스에게 자신이 종료되고 있다고 알림
      프로세스의 실행 상태를 task_strcut 구조체의 state 필드의 TASK_DEAD로 설정
      do_task_dead() 함수를 호출해 스케쥴링을 실행
      do_task_dead() 함수에서 __schedule() 함수가 호출되어 프로세스 자료구조 태스크 디스크립터와 스택 메모리를 해제

      do_task_dead() 함수

- 종료할 프로세스는 do_exit() 함수에서 대부분 자신의 리소스를 커널에게 반납하고 자신의 상태를 TASK_DEAD로 변경
- 컨텍스트 스위칭을 한다.
- 컨텍스트 스위칭으로 다음에 실행하는 프로세스는 finish_task_switch() 함수에서 이전에 실행했던 프로세스 상태가 TASK_DEAD이면 프로세스 스택 공간을 해제
- 이렇게 동작하는 이유는 process가 스스로 자신의 메모리 공간을 해제하지 못하므로 스위칭을 수행 후 다음에 실행되는 process에게 자신의 스택 메모리 공간을 해제하고 소멸시키도록 동작함


<br/>

## 함께보기
- [동기화 문제](https://github.com/t0e8r1r4y/blogContents/blob/main/OSConcepts/ProcessSynchronization.md)
