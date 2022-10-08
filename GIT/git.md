# Git과 GitHub

## 목적
- git과 github 사용과 관련해서 내용을 정리하고 참고자료를 정리합니다. 브랜치 관리를 `잘` 합시다.

## 용어 정리( git과 github 차이점 )
- git : 로컬 파일의 변경사항을 기록하고 해당 파일에 대한 여러  사용자 간의 작업을 조율하기 위한 버전 관리 시스템이다.
- github : 깃을 클라우드 방식으로 구현한 버전 관리 시스템.

## git branch 관리 관련 명령어
- `Local` branch 정보 조회 ( *위치가 현재  위치 )
```
$ git branch
* feature3
  main
  ticket-user
```
- `Remote` branch 정보 조회
```
$ git branch -r
  origin/feature1
  origin/feature2
  origin/feature3
  origin/main
```
- `Local` branch의 정보를 마지막 커밋 내역과 함께 조회
```
git branch -v
```
- `Local/Remote` branch 정보 모두 조회
```
git branch -a
```
- `Local` branch와 매칭된 원격 브랜치 정보 함께 조회
```
git branch -vv
```
- `Local` branch 생성
```
git branch (이름)
```
- `Local` branch 생성과 동시에 해당 branch로 이동하는 방법
```
git checkout -b (이름)
```
- `Local` branch 제거 ( 아직 merge하지 않은 커밋을 담고 있는 경우 강제삭제만 가능 )
```
git branch -d (브랜치명)
```
- [중요] 원격에 있는 branch 가져오기
    - `-b` 옵션을 주면 내가  지정한 로컬  브랜치에 원격 브랜치를 연결함
    - `-t` 옵션을 주면 원격 브랜치명을 그대로  local에 생성하면서 브랜치를 연결함
```
git checkout -b (로컬브랜치) (원격브랜치)
git checkout -t (원격 브랜치)
```



## 참고자료
- [git 브랜치 학습 게임](https://learngitbranching.js.org/?locale=ko)
- [git 브랜치 관리 공식문서](https://docs.github.com/en/issues/tracking-your-work-with-issues/creating-a-branch-for-an-issue)
