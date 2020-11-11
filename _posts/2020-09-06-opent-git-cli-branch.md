---
layout: post
title: Git CLI Branch & Conflict
subtitle: 생활코딩 Git CLI Branch & Conflict 정리노트
categories: StudyNote
tags: [Git, CLI, Branch, Conflict, 생활코딩, 정리노트]
---

*본 포스트는 필수 개발 도구인 Git의 가지(Branch) 및 충돌(Conflict)에 대한 정리노트입니다.*

*포스트 내 모든 내용은 [생활코딩 - Git CLI - Branch & Conflict 수업][git-cli-branch]에 기반하고 있습니다. 아래 내용은 해당 강좌에 대한 내용 정리입니다.*

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
[git-cli-branch]: https://opentutorials.org/course/3840


***



## 0 커버페이지

버젼 관리란? : 신규 버젼으로 계속 업데이트하는 것

만약, 고객이 여러명으로 다른 버젼이 각기 필요하다면?

* 이 때 필요한 기능이 **가지(Branch)**
  * 하나의 뿌리에서 나온 여러 다른 버전들
  * **충돌(Conflict)** 문제 발생은 필연적

### 0.1 실습준비

~~~Terminal
$ mkdir manual
$ cd manual
$ git init
$ ls -al

$ nano work.txt  # content1 추가하고 저장
$ git status
$ git add work.txt
$ git commit -m "work1"
$ git log  # 동일한 작업을 work3까지 3번 반복.

$ git log -p
~~~


## 1 브랜치의 사용법

`git log --all --graph --oneline`   
  * `--all` 모든 버젼을 보여줌
  * `--graph` CLI환경에서 아스키 그래프를 표현
  * `--oneline` 한줄로 줄여줌   

`git branch`		현재 브랜치 정보를 보여줌   
`git branch BRANCH_NAME`		신규 브랜치를 생성

~~~Terminal
$ git branch apple; git branch google; git branch ms  # apple, google, ms 브랜치 생성
$ git branch

$ nano work.txt
	content1
	content2
	content3
	master content4  # 신규 추가 후 저장

$ git commit -am "master work4"

$ git checkout apple  # apple 브랜치로 변경 (commit #3로 이동)
$ nano work.txt
	apple work4  # 신규 추가 후 저장
$ nano apple.txt
	apple work4  # 신규 추가 후 저장
$ git add .	현재 디렉토리 파일 모두 추가
$ git commit -m "apple work4"
$ git log --all --graph --oneline  # 아스키 그래프로 log 확인

# 동일 작업을 google, ms 브랜치에서도 실시한 후, git log 확인할 것
~~~

## 2 병합 - Merge

### 2.1 브랜치 병합

**base** : 브랜치가 나오기 전 원래 가지   

`git merge BRANCH` 브랜치 병합

~~~Terminal
### 실습 - 다른 파일을 병합

$ git init manual-merge; cd manual-merge
$ nano work.txt
	1  # 신규 내용 작성 후 저장
$ git add work.txt; git commit -m "work1"; git log

$ git branch o2  # o2 브랜치를 생성
$ nano master.txt
	2
$ git commit -am "work2"
$ git commit --amend  # 기존 커밋 메시지 변경
	master work2 # 메시지 변경 후 저장

$ git checkout o2  # o2 브랜치로 이동. "master work2" commit은 반영되어 있지 않음.
$ nano o2.txt
	o2
$ git add o2.txt
$ git commit -m "o2 work2"

$ git checkout master  # 병합 전 base 브랜치로 이동
$ git merge o2  # 기존 master에 o2 내용이 병합

$ git reset --hard PREVIOUS_COMMIT_ID
  # 기존 상태로 회귀. 반복하여 merge 테스트 할 것 (익숙해 질 때까지)
~~~

~~~Terminal
### 실습 - 기존 파일의 내용만 수정된 경우 병합

$ git init manual-merge2; cd manual-merge2
$ nano work.txt
	title
	upper content

	title
	lower content2  # 신규 작성 후 저장
$ git add work.txt
$ git commit -m "work1"

$ git branch o2
$ nano work.txt
	# upper content --> master content로 내용 변경 후 저장
$ git add work.txt; git commit -am "master work2"

$ git checkout o2
$ nano work.txxt
	# lower content --> o2 content로 내용 변경 후 저장
$ git add work.txt; git commit -m "o2 work 2"

$ git checkout master
$ git merge o2
$ cat work.txt  # master와 o2가 모두 들어가 있는 내용으로 변환
~~~

~~~Terminal
### 실습 - 기존 파일의 동일한 내용이 수정된 경우 병합 ==> 충돌

$ git init manual-merge3;cd manual-merge3
$ nano work.txt
	#title
	content
$ git add work.txt; git commit -m "work1"

$ git branch o2
$ nano work.txt
  마지막 줄 master 추가 후 저장
$ git commit -am "master work2"

$ git checkout o2
$ nano work.txt
  마지막 줄 o2 추가 후 저장
$ git commit -am "o2 work2"; git log

$ git checkout master
$ git merge o2
$ git status
$ nano work.txt  # 충돌 내용이 표시됨
	master, o2로 바꾸고 나머지 추가 내용은 삭제

$ git add work.txt
$ git status
$ git commit  # 충돌이 해결된 후 다시 재커밋 발행
$ git log
~~~


### 2.2 3-way merge

* 2 way merge :	2개의 브랜치를 비교해서 일치하는 부분만 병합, 나머지는 충돌
* 3 way merge	: Base와 2개의 브랜치를 비교해서 수정된 부분은 전부 병합, 베이스에서 각각 다르게 변경된 경우만 충돌

(예제) BASE에서 hear, there 각 브랜치로 변경된 후 병합할 경우,

|here|**BASE**|there|=merge=>|2-way|**3-way**|
|:---:|:---:|:---:|:---:|:---:|:---:|
|A|A|A|-->|A|A|
|H|B|B|-->|충돌|B|
|C|C|T|-->|충돌|C|
|H|D|T|-->|충돌|충돌|


### 2.3 외부 도구를 이용하여 병합

외부도구를 이용해서 좀 더 편하게 충돌을 확인하고 수정할 수 있다.   
Google에서 `3-way merge tool` 검색할 것.

* p4Merge 사용법
  1. Google > "p4Merge" 검색
  2. PERFORCE > p4Merge 다운로드
  3. Terminal > git config --global merge.tool p4mergetool
    * ~/.gitconfig 내 tool 설정이 p4Merge로 변경
    * cat ~/.gitconfig
  4. git mergetool


## 3 (부록) reset vs checkout

* HEAD : 기본적으로 HEAD --> master
  * 현재 HEAD가 master branch를 checkout
  * 보통 master 등 branch를 지시
  * HEAD는 branch가 아니라 바로 commit 버전을 지시할 수도 있음.<br>이 경우, 해당 버젼으로 저장소가 바뀜. 이를 'detached'라고 함.

| Vs.|checkout|reset|
|---|---|---|
|conrol|HEAD가 무엇을 가르키고 있는지를 지시 (HEAD를 제어)|HEAD가 branch를 가르키고 있다면 branch를 제어|
|master|`checkout master`<br>HEAD를 master로 변경|`reset master`<br>현재 branch를 master와 동일하게 변경<br>이전 작업은 삭제|
|point|보통 branch을 지시|보통 commit을 지시 (기존 버젼은 삭제된 같은 효과)|



## 4 수업을 마치며

egoing 선생님이 추천해 주는 추가로 공부하면 좋을 git 관련 주제

* git workflow
  * git flow : 개발자 모범사례
* chrry-pick
* rebase
