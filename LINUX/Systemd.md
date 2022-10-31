# System Management rc.local 시작 스크립트 활성화 방법

> 관련 글을 [미디엄 블로그](https://medium.com/@tas.com/ec2-reboot-%EC%8B%9C-%EC%9E%90%EB%8F%99%EC%9C%BC%EB%A1%9C-%EC%84%9C%EB%B2%84-%EA%B5%AC%EB%8F%99-%EC%8B%9C%ED%82%A4%EA%B8%B0-rc-local-%EC%82%AC%EC%9A%A9-985a92b981c)에도 한번 정리를 했는데 git에도 남겨둡니다.  
> 해당 글은 아마존 리눅스에서 사용한 예시 입니다.


<br>

## rc.local이란?
- 부팅 시 자동실행 명령어 스크립트를 수행하며 일반적으로 서버 부팅시마다 매번 자동으로 실행되길 원하는 명령어를 추가하는 곳입니다.
- 부팅 시 가장 나중에 적용 됩니다.

<br>

#### 리눅스 부팅 과정과 rc.local 실행
1. 전원 인입
2. ROM BIOS에서 지정된 부트 드라이브로 부팅 시작
3. boot sector load
4. GRUB 동작
5. Kernel image load
6. file system mount
7. init process 동작

> 아마존 리눅스의 경우 Init process는 inittab을 더 이상 사용하지 않고 systemd를 사용한다고 함
```
# inittab is no longer used when using systemd.
#
# ADDING CONFIGURATION HERE WILL HAVE NO EFFECT ON YOUR SYSTEM.
#
# Ctrl-Alt-Delete is handled by /usr/lib/systemd/system/ctrl-alt-del.target
#
# systemd uses 'targets' instead of runlevels. By default, there are two main targets:
#
# multi-user.target: analogous to runlevel 3
# graphical.target: analogous to runlevel 5
#
# To view current default target, run:
# systemctl get-default
#
# To set a default target, run:
# systemctl set-default TARGET.target
```


<br>

## 사용법
- /etc 경로에서 rc.local 파일에 실행 해야 될 shell을 추가한다.
```Shell
#!/bin/bash
# THIS FILE IS ADDED FOR COMPATIBILITY PURPOSES
#
# It is highly advisable to create own systemd services or udev rules
# to run scripts during boot instead of using this file.
#
# In contrast to previous versions due to parallel execution during boot
# this script will NOT be run after all other services.
#
# Please note that you must run 'chmod +x /etc/rc.d/rc.local' to ensure
# that this script will be executed during boot.

touch /var/lock/subsys/local
```

- rc.load에 등록하기
  - 작성한 쉘스크립트를 /etc/rc.d 경로에 넣어준다.
  - su root -c "/etc/rc.d/startup.sh &>/dev/null &"를 입력해서 콘솔에 print 하지 않도록 추가 ( 선택 )
- rc.local 실행 권한 부여 ( chmod 명령어 사용 )
- rc-local.service 파일 편집
  - 마지막줄에 아래 내용 추가
  ```shell
  [Install]
  WantedBy=multi-user.target
  ```
  
- 서비스 실행
  - sudo systemctl --now enable rc-local.service



