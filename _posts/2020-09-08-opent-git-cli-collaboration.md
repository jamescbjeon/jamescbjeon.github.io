---
layout: post
title: Git CLI 협업
subtitle: 생활코딩 Git CLI 협업 정리노트
categories: Git
tags: [Git, CLI, Collaboration, 생활코딩, 정리노트]
---

*본 포스트는 필수 개발 도구인 Git의 협업(Collaboration)에 대한 정리노트입니다.*

*포스트 내 대부분의 내용은 [생활코딩 - Git CLI - 협업 수업][git-cli-collaboration]에 기반하고 있습니다. 아래 내용은 해당 강좌에 대한 내용 정리입니다.*

> 생활코딩 Git CLI 정리노트   
  1. [Version - 버전관리][git1]
  1. [Branch & Conflict - 가지 및 충돌][git2]
  1. [Back-up - 백업][git3]
  1. [Collaboration - 협업][git4]
  1. ~~Cherry pick & rebase~~
  1. ~~Github pull request~~

[git1]: https://jamescbjeon.github.io/Git/2020/09/05/opent-git-cli-version.html
[git2]: https://jamescbjeon.github.io/Git/2020/09/06/opent-git-cli-branch.html
[git3]: https://jamescbjeon.github.io/Git/2020/09/07/opent-git-cli-backup.html
[git4]: https://jamescbjeon.github.io/Git/2020/09/08/opent-git-cli-collaboration.html
[git-cli-collaboration]: https://opentutorials.org/course/3842

***

## 0 커버페이지

협업을 위해서는 다음 2가지에 대한 사전 지식 필요

1. [git backup][git3]
2. [git branch][git2]

## 1 git으로 혼자 작업하기

> Remote repo를 중심으로 여러 장소에서 마치 Cloud 환경처럼 작업하기

`git remote add origin REMOTE_URL` 원격 저장소 연결`

`git push -u origin master` Local master와 Remote master를 페어링 해주는 작업 (-u)

## 2 git으로 같이 작업하기

오픈소스는 누구나 다운로드 가능하지만, push를 하려면 승인 필요

> 권한 취득 :    
Github repo > Setting > Collaborator 추가 (e-mail) > 이메일 확인 승인

~~~Terminal
# Github > 필요 Repo > CLONE-URL 복사
$ git clone CLONE-URL MY_REPO_NAME  # MY_REPO_NAME은 필요대로 지정
~~~

~~~Terminal
# 충돌 발생 예시. 서로 동일한 위치를 2명 이상이 작업 후 각각 push한 경우,

$ git push	--> rejected. pull 후 push하라는 error 발생
$ git pull	--> 충돌 발생

# 충돌 수정 후,
$ git add work.txt
$ git commit
$ git push	--> 작업이 서로 일치
~~~


## 3 git pull vs fetch 그리고 원격브랜치

`git pull` == `git fetch` + `git merge FETCH_HEAD`   
`git pull` == `git fetch; git merge origin/master`

* 다음 2가지 작업 결과는 동일
  1. git pull --> commit --> push
  2. git fetch --> git merge FETCH_HEAD --> commit --> push

~~~Terminal
# 이해를 위한 2가지 발생 가능 예제

# case1
$ git log
	HEAD -> master
	origin/master
  # local이 remote보다 commit이 앞 단계에 위치. push로 동기화 필요

# case2
$ git fetch
	origin/master
	HEAD -> master
  # local이 remote보다 commit이 뒷 단계에 위치. pull 또는 merge origin/master로 동기화 필요
~~~

`git fetch`는 Remote repo에서 Local repo를 업데이트만 하고, HEAD가 가리키는 위치는 변화 시키지 않음. 반면, `pull`은 HEAD 위치까지 전부 변경함.

이 때 branch를 찾아서 명령을 하면 불편한데, fetch를 할 때, FETCH_HEAD가 자동 생성. 따라서 `git merge FETCH_HEAD`하면 동일한 효과가 발생

즉, 신중하게 `git pull`하고 싶을 때는 우선 `fetch`한 후 점검 한 다음 `merge`하면 된다. ~~*보통은 pull로 작업하지만*~~

## 4 수업을 마치며

egoing 선생님이 추천하는 추가로 공부하면 좋을 git 관련 주제

* code review
  * [gerrit][gerrit] : 안드로이드 오픈소스 개발툴. push 때 바로 병합되지 않고 투표소 이동 및 확인 후 병합.
  * [issue tracker][issue-tracker]

[gerrit]: https://www.gerritcodereview.com/
[issue-tracker]: https://www.zendesk.com/blog/issue-tracker/
