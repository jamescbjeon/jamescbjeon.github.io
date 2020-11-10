---
layout: post
title: Git CLI 버전관리
subtitle: 생활코딩 Git CLI 버전관리 정리노트
categories: markdown
tags: [Git, CLI, 버전관리, 생활코딩, 정리노트]
---

*본 포스트는 필수 개발 도구인 Git의 버전관리에 대한 정리노트입니다.*

*포스트 내 모든 내용은 [생활코딩 - Git CLI - 버전관리 수업][git-cli-version]에 기반하고 있습니다. 아래 내용은 해당 강좌에 대한 내용 정리입니다.*

> 생활코딩 Git CLI 정리노트   
  1. [Version - 버전관리][git1]
  1. [Branch & Conflict - 가지 및 충돌][git2]
  1. [Back-up - 백업][git3]
  1. [Collaboration - 협업][git4]
  1. ~~Cherry pick & rebase~~
  1. ~~Github pull request~~

[git1]: https://jamescbjeon.github.io/markdown/2020/09/05/opent-git-cli-version.html
[git2]: https://jamescbjeon.github.io/markdown/2020/09/06/opent-git-cli-branch.html
[git3]: https://jamescbjeon.github.io/markdown/2020/09/07/opent-git-cli-backup.html
[git4]: https://jamescbjeon.github.io/markdown/2020/09/08/opent-git-cli-collaboration.html
[git-cli-version]: https://opentutorials.org/course/3839

***

## Cheatsheet

`git init`	Initialize repository   
**.git**		git repository (로컬저장소)

`git status`	working tree status

`git add FILE_NAME`		add to staging area   
`git add .`   add all file to staging area   
`git commit`	create version

`git log`		show version   
`git log --stat`   show version statics   
`git log -p`  show version patch == diff   
`git diff`	show changes

`git checkout`     
`git reset --hard`   
`git revert`

`git config --global core.editor "vim"`  git 기본 에디터를 vim으로 변경   
`git config --global core.editor "nano"`  git 기본 에디터를 nano로 변경

***

## 0 커버페이지

왜 Command Lind Ineterface를 사용하는가?
* CLI는 입문은 어렵지만, 알고나면 아래의 장점을 갖음 : [Posix CLI 정리][blog-posix-cli]
  * 한번에 여러 명령을 일괄처리 가능
  * GUI 없는 서버 등 환경에서도 사용 가능
* ~~단, Terminal 지옥에 익숙해야 한다는 함정~~

> GUI 기반의 SourceTree나 Github Desktop도 많이 쓰이고 있음. 단, git 자체가 CLI 기반으로 제작되어 사용이 편리한 편(?)이며, CLI로 기본을 익히면 GUI 환경에서 좀 더 풍부한 이해로 작업할 수 있음. 관련 GUI clients는 [git GUI clients 바로가기][git-gui-clinets]를 참조.

## 1 git 준비

### 1.1 git 설치

1. 설치유무 확인

~~~Terminal
$ git
~~~

2. 설치되지 않은 경우, [git Homepage][git-hp]에서 패키지 다운로드 및 설치
3. Terminal 재시작


### 1.2 버전관리의 시작

`git init`  Initialize git (git 생성)   
`git init .`  '.'는 현재 디렉토리. 즉, 현재 위치에서 git 생성

~~~Terminal
$ mkdir hello-git-cli;cd hello-git-cli;ls -al # 신규 폴더 생성 및 이동 후 점검
$ git init .  # 해당 위치에 git 생성
$ ls -al  # list 확인 시, '.git'이라는 신규 git repository가 생성. 향후 git 작업은 해당 repository에서 진행.
$ cd .git
$ cd ..
~~~

## 2 버전의 개념

### 2.1 버전의 생성

* 개념

|Stage|Pointer|상태|
|---|---|---|
|**Working tree**|Workig Directory|아직 버젼으로 만들기 전 단계|
|**Staging area**|Index|버젼을 만들려 하는 수정 파일|
|**Repository**|HEAD|저장소. 즉, 버젼이 완성된 파일들|

* git 처리 순서
  1. 개발 시작 : 아직 Working tree 단계. `git status`로 이전 버젼과 차이 유무 확인 가능.
  2. 작업 완료 : `git add`를 통해 필요한 파일을 Staging area에 추가
  3. 최종 반영 : `git commit`으로 신규 버젼을 반영함. commit된 파일만이 버전으로 등록되며, 이를 통해 버전 회귀 (reset, revert), 가지치기 (branch), 백업/협업 (pull/push) 등이 가능

`git status` Working tree 상태 확인

`git add FILE_NAME` 작업 사항을 Staging area에 반영   
`git add .` '.'은 모든 파일 추가를 의미

`git commit -m COMMIT_MESSAGE` Staging area에 추가된 파일을 최종 버젼에 반영

`git log` Commit 이력 및 Commit ID를 확인   
`git log --stat` Commit 관련 상세 파일 이력 확인 (수정된 파일의 통계정보)
`git log -p` 각 Commit의 diff 결과 (적용된 패치Patch 조회)

~~~Terminal
$ nano hello1.txt  # hello1.txt 생성. 내용 작성 후 저장
$ cat hello1.txt  # 내용 확인

$ git status
    # Working tree 상태 확인
      # No commits yet : 아직 버젼이 없음을 의미
      # Untracked files: .. : 버젼관리가 아직 되지 않는 파일을 표시

$ git add hello1.txt	# 해당 파일을 Staging area에 반영 요청.
$ git status
	 # Changes to be committed ... : 변경 사항이 있음을 의미

$ git commit -m "Message1"
  # 신규 버젼 생성. -m은 message 옵션이며 참고 코멘트를 추가 가능. commit을 통해서 해당 버젼은 repository로 이동.

$ git status
  # nothing to commit, working tree clean : commit 이후로 추가된 작업이 없음. 즉, 현재 working tree가 비어있어 추가 commit이 필요하지 않음.

$ git log	 # commit 관련 이력 출력, 'q'를 누르면 종료

$ nano hello1.txt  # hello1.txt를 수정. 추가 내용 작성 후 저장
$ git status
	 # Changes not staged for commit : Commit되지 않은 신규 작업이 있음
$ git add hello1.txt
$ git commit -m "Message2"
$ git status
$ git log

$ nano hello1.txt	 # hello1.txt를 수정. 추가 내용 작성 후 저장
$ nana hello2.txt  # hello2.txt라는 신규 파일 생성
$ git status
$ git add .  # 모든 변경사항을 반영
$ git commit -m "Message3"

$ git log  # 3개의 버젼이 commit 됨을 확인 가능
$ git log --stat
~~~


### 2.2 버전간의 차이점 비교

`git diff`  이전 버젼과 차이점 비교. 'git log -p'로도 가능

`git reset`  기존 commit으로 원복   
`git reset --hard`  --hard의 경우, 기존 commit으로 원복되며 이후에 실행된 모든 commit은 삭제. 즉, 다시 현재 상태로 올 수 없음.

~~~Terminal
$ nano hello1.txt  # hello1.txt를 수정 후 저장
$ git status
$ git diff	#	이전버젼과 차이점을 비교

$ git reset --hard	 # 지금까지 작업했던 내용 삭제
$ git log -p  # 기존 commit 시점으로 원복되며, 작업 사항은 모두 삭제됨을 확인
~~~

## 3 버전 이동

### 3.1 checkout과 시간여행

`git checkout COMMIT_ID/BRANCH`  해당 commit_ID 혹은 branch로 이동   

> git checkout은 reset이 아니며, 해당 시점으로 INDEX를 이동시켜 마치 시간여행 하듯이 작업 사항을 변경시켜 주는 명령. 즉, 원하는 위치로 계속 이동 가능하며, 이 때 기존 작업사항은 그대로 유지됨.

~~~Terminal
$ ls -al
$ cat hello1.txt
$ cat hello2.txt  # 현재 상태의 hello1,2.txt를 확인

$ git log  # 원하는 시점의 commit_ID를 복사 후 q를 눌러 복귀할 것
$ git checkout commit_ID  # 해당 시점으로 버젼 변경

$ ls -al
$ git log
$ cat hello1.txt  # 해당 시점으로 모든 파일이 바뀜을 확인가능

$ git checkout master	 # 가장 최근의 시점으로 원복 (master branch)
$ ls -al  # 모두 원복됨을 확인 가능
~~~

### 3.2 버전 삭제, reset

`git reset COMMIT_ID` 해당 시점으로 HEAD 브랜치를 이동   
`git reset --hard COMMIT_ID` HEAD 브랜치를 해당 commit을 이동하고 working directory까지 전부 업데이트. 복원 불가.   
`git reset --help` reset 관련 설명

> reset과 checkout은 유사한 부분이 많아 정확한 이해가 필요. 관련 내용은 [참고자료 - git reset 명확히 알고 가기][git-reset]를 참조

~~~Terminal
$ git log
$ git reset --hard commit_ID  # 해당 commit 시점으로 원복
$ git log
~~~

### 3.3 버전 되돌리기, revert

`git revert COMMIT_ID`	해당 시점 직전으로 원복하는 신규 commit을 발행

> revert로 직전 commit이 아니라 여러 commit 이전으로 가고 싶다면, 해당 시점까지 발생된 commit을 단계적으로 revert해서 접근해야 함. 그렇지 않으면 충돌(conflict)이 발생. 왜냐하면 git revert는 해당 시점으로 변경되는 게 아니라 commit 발생시점에서 확인된 변화(patch)만 원복되는 것이므로.

~~~Terminal
$ git revert commit_ID 	# 해당 커밋을 취소하고 직전 버전으로 복귀
$ git log
$ git diff
~~~


## 4 수업을 마치며

egoing 선생님이 추천해 주는 추가로 공부하면 좋을 git 관련 주제

* diff tool : 차이점을 비교할 수 있는 도구
* .gitignore : 버젼 변경을 하지 말아야 할 중요한 파일을 보관하는 법
* branch : 다음 수업 주제
* tag :	commit_ID는 알아보기 힘드므로 쉬운 이름을 붙여 중요한 버젼을 찾아갈 수 있도록
* backup : 다음 수업 주제		

[blog-posix-cli]: https://jamescbjeon.github.io/markdown/2020/09/01/opent-posix-cli1.html
[git-hp]: https://git-scm.com/
[git-gui-clinets]: https://git-scm.com/downloads/guis
[git-reset]: https://git-scm.com/book/ko/v2/Git-%EB%8F%84%EA%B5%AC-Reset-%EB%AA%85%ED%99%95%ED%9E%88-%EC%95%8C%EA%B3%A0-%EA%B0%80%EA%B8%B0
