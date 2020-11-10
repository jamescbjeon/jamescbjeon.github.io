---
layout: post
title: POSIX CLI
subtitle: 생활코딩 Posix CLI 정리노트
categories: markdown
tags: [POSIX, CLI, Unix, 생활코딩, 정리노트]
---

*본 포스트는 Unix 계열을 통칭하는 POSIX의 Command Line Interface에 대한 정리노트입니다.*

*포스트 내 모든 내용은 Opentutorials - Posix CLI1 수업에 기반하고 있습니다. 45분 정도의 YouTube 강좌이니 CLI가 생소하거나 이제 막 입문하려는 컴린이들은 직접 수강하는 것을 권합니다.*

Opentutorials - Posix CLI1 강좌 : <https://opentutorials.org/module/3747>

---

## 0 커버페이지

* What is **Interface**?
	* 컴퓨터와 대화하는 방법
	* 2가지 가능
		1. 직접 대화 - `CLI`, *Command Line Interface*
		2. 간접 대화 - `GUI`, *Graphical User Interface*


* Why **CLI**?
	1. 시간의 순서에 따라 명령을 내릴 수 있음
	2. GUI 대비 자원 소모가 없음. 즉, Resource 낭비 방지
	3. 사용자 접근이 제한되는 Server 등은 거의 CLI로만 구동


* **POSIX**, *Portable Operating System Interface*
	* Unix계열의 운영체제를 다루기 위한 표준
		* 즉, Unix / Linux / MacOS에서 혼용 가능. ~~일부 차이는 있지만...~~
	* Windows의 경우는 별도
		* CMD, Powershell이라는 별도 표준이 존재
		* Emulator를 이용하면 Windows도 제어 가능


### 0.1 명령어 실행환경 준비

* 환경 준비
	* Unix, Linux, MacOs : Terminal
	*	Windows, IOS, Android : Emulator, Secure shell
		* POSIX 환경이 아니므로 별도 우회가 필요


## 1 수업소개

컴퓨터에서 가장 중요한 다음 2개 항목을 어떻게 제어하는지 공부

> 1. File   
> 2. Directory

|Func.|기능| File | Directory |
|---|---|---|---|
|Create |생성 |*editor* |`mkdir` |
|Read |읽기 |*editor*<br>`cat`, `ls` |`ls` |
|Update |수정 |*editor*<br>`mv` |`mv` |
|Delete |삭제 |`rm` |`rm -r` |


## 2 디렉토리 - Directory

### 2.1 디렉토리의 사용

`pwd` print working directory, 현재 작업 디렉토리 표시
* `/` 	*Root directory*
* `~`	*Home directory*
* `./`	*. (dot)은 현재 디렉터리를 의미*
* `../`	*Parent directory, 즉 현재 바로 상위 디렉토리*

`cd`	Change directory
* `cd /` *Root directory로 이동*
* `cd ~` *Home directory로 이동*
* `cd /example/dir` *명기된 디렉토리로 바로 이동*


### 2.2 현재 디렉토리의 상태보기와 명령어의 형식

> `명령어 --help` 또는 `man 명령어`로 관련 command 설명 확인 가능   
화살표로 위아래 내용 조회, 'q'를 눌러 탈출

`touch FILE_NAME` 빈 파일 생성 (make empty file)

`ls`	list, 현재 디렉토리 내 파일 및 디렉토리 목록을 반환
* `ls -l`	*List in long format*
* `ls -a`	*Show all files including hidden files*
* `ls -a -l`, `ls -al` *-a, -l 옵션을 같이 사용. 이때 한 번에 -al로도 가능*

> `.FILE_NAME`	hidden file   
*POSIX에서는 파일명 앞에 '.'이 있으면 숨김파일로 인식   
Windows의 경우, 명시적으로 숨김을 표기해야 함*


### 2.3 디렉토리의 생로병사

`mkdir 디렉토리명`	Make directory, 신규 디렉토리를 생성

`./` 현재 디렉토리

`mv 기존이름 새이름`	Move, 디렉토리 이름 변경

`rm -r 디렉토리명`	Remove, 디렉토리 삭제

> *File과 달리 디렉토리 rm(remove)은 실수 방지를 위해 -r 옵션을 필요로 한다. 참고로 -r은 remove file hierarchies를 뜻함*


### 2.4 절대경로 vs. 상대경로

`cd /`	최상위 디렉토리 (Root directory)로 이동

`cd ..`	바로위 디렉토리로 이동 (cd ../과 동일)   
> *`cd ./` 가 현재 디렉토리이기 때문에 `..`이면 이전 디렉토리 (parent directory)*

* 경로, Path
	* 절대경로 (Absolute path)&nbsp;&nbsp;&nbsp;&nbsp;현재 위치에 관계없이 고정
	* 상대경로 (Relative path)&nbsp;&nbsp;&nbsp;&nbsp;현재 위치에 따라 변함

> *Example @ `pwd	/Users/Ex-dir`에서*   
> 상대경로 참조 이동 :  `cd ./posix`   
> 절대경로 참조 이동 :  `cd /Users/Ex-dir/posix`


## 3 파일 - File

### 3.1 파일생성과 읽기

파일은 적절한 *Editor* 로 생성한다. *(Ex. nano, vim ...)*

`nano hello.txt`	*hello.txt* 문서를 생성 혹은 수정

`cat hellot.txt`	*hello.txt* 문서의 간단한 조회

> *`nano`는 GNU 기반의 간단한 텍스트 에디터*   
> *`cat`은 concatenate의 약자로 파일안의 컨텐츠를 출력하거나 파일들을 이어 주는 명령어*


### 3.2 파일수정과 삭제

`nano 문서이름.txt` *nano editor로 해당 문서 수정 (없을 경우, 신규 생성)*

`mv 기존이름 새이름`	*파일 이름 변경*   
`mv 파일이름 ../파일이름`		*디렉토리 변경하면서 파일 이동*

`CTRL+C` **명령 취소** *, 입력값은 실행되지 않음*   

`파일이름 일부 작성 후 'TAB'`	*자동완성*

`clear`	*화면 지우기*

`rm 파일이름` *파일 삭제*


## 4. Command Line Interface

### 4.1 GUI vs. CLI

CLI가 갖는 또 하나의 놀라운 장점
1. **풍부하고 정확한 내용**을 지시/전달할 수 있음
1. 원하는 명령을 **순차적으로 한 번에 지시** 가능


### 4.2 순서대로 실행하기

명령과 명령 사이는 ;으로 구분하면 한 번에 Command 적용 가능

`(ex) mkdir dummy;cd dummy;touch hello.txt;cd..;ls -R`


### 4.3 자동화 - 실패하면 실행 멈추기

위의 순차 적용은 실패할 경우, 다음 command로 자동이동

`&&` 	AND operator   
`;` 대신 `&&` 사용하면 앞의 명령어가 성공했을 경우만 이후 명령이 실행


## 5. 수업을 마치며

egoing 선생님이 추천하는 추가로 공부하면 좋을 주제

* Program : 	Shell script
* Pacakge manager :	(MAC) homebrew
* Maintain : (Storage/Memory/Processor) --> top, htop
	* 컴퓨터 구조에 대한 공부 (Computer architecture)
* Network		네트워크 설정/관리
