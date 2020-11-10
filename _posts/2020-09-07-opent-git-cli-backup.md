---
layout: post
title: Git CLI Backup
subtitle: 생활코딩 Git CLI Backup 정리노트
categories: markdown
tags: [Git, CLI, Backup, 생활코딩, 정리노트]
---

*본 포스트는 필수 개발 도구인 Git의 백업(Backup)에 대한 정리노트입니다.*

*포스트 내 대부분의 내용은 [생활코딩 - Git CLI - Backup 수업][git-cli-backup]에 기반하고 있습니다. 아래 내용은 해당 강좌에 대한 내용 정리입니다.*

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
[git-cli-backup]: https://opentutorials.org/course/3841

***

## 0 커버페이지

## 1 수업의 목표와 용어정리

* Repository(저장소) 연결
	* `push` : Local repository --> Remote repository
	* `clone` : Remote repository --> Local repository (new)
	* `pull` : Remote --> Local (old)

### 1.1 Git hosting

* git hosting	: 원격 저장소를 임대
	* 원격 서버 유지는 상당한 노력이 필요하므로 보통 관련 서비스를 이용

* [git hosting 검색][git-hosting-compare]해서 제공 서비스를 서로 비교해 볼 것
	* (대표 서비스) github, gitlab

### 1.2 공부의 방향

* Where to where?
	1. Local to remote
	1. Remote to local

* How connect?
	1. HTTP : 보안적으로는 다소 취약. 배울 필요 없음.
	1. SSH : 보안성 높음. 배우기 어렵고, 다소 난해

> 일단 간단한 http로 시작하고, 익숙해 진 후 보안문제에 만나면 SSH는 별도 공부하자

## 2 [원격저장소][git-remoterepo]와 연결

* 일반적인 작업 순서
	* `git pull` --> 작업 --> `git add` --> `git commit` --> `git push`

### 2.1 git push

`git remote -v`	현재 연결된 Remote repository 확인. `-v`는 주소 표기 옵션

`git remote add origin REMOTE_URL` Remote URL에 'origin'이라는 이름으로 Repo 연결

`git push` local --> remote repository로 파일 전송/동기화   
`git push -u origin master`

> Local to remote가 이미 연결되어 있으면 문제 없이 완료

> 최초 연결 시, `git push --set -upstream origin master` 에러 발생 시,   
* Local repository를 Remote repository 중 어떤 것에 연결할 건지 git이 물어보는 것
* 상기 에러 명령어대로 입력 후 재실행. Github ID/PW 입력

~~~Terminal/Example
$ nano hello1.txt		# 신규 생성 후 저장
$ git status
$ git add hello1.txt
$ git commit -am "backup"

$ git push  # ID/PW 필요 시, 입력
~~~

### 2.2 git clone

`git clone REMOTE_REPO_ADDRESS` 지정된 Remote repository에서 현재 디렉토리로 Local repo 복제

~~~Terminal/Example
$ pwd  # 현재 위치 확인
$ git	 # git 설치 확ㅇ린

## Github 접속 > Repo > 'Clone or download (녹색 버튼)' > HTTPS link copy

$ git clone COPIED_ADDRESS (REQUIRED_DIR_NAME)  # 원격저장소 복제. 주소 뒤에 Local repo 이름은 변경 가능/혹은 생략
~~~

### 2.3 git pull

`git pull` 연결된 Remote repository에서 데이터 복제 및 동기화

## 3 git과 오픈소스

## 4 수업을 마치며

egoing 선생님이 추천해 주는 추가로 공부하면 좋을 git 관련 주제

* SSH	저장소 간 통신 방법 : 자동으로 로그인 가능
* github/gitlab	기능을 꼼꼼히 살펴보자
	* 예. issue tracker
* [협업/conflict][git4] : 충돌을 어떻게 해결할 것인가

[git-hosting-compare]: https://comparegithosting.com/
[git-remoterepo]: https://git-scm.com/book/ko/v2/Git%EC%9D%98-%EA%B8%B0%EC%B4%88-%EB%A6%AC%EB%AA%A8%ED%8A%B8-%EC%A0%80%EC%9E%A5%EC%86%8C#_remote_repos
