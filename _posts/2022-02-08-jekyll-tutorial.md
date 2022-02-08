---
layout: post
title: Jekyll - Static Site Generator
subtitle: Youtube Tutorial 공부노트
categories: Jekyll
tags: [Jekyll, GitPage, Blog, Ruby Gem]
---

[ghpage]: https://pages.github.com/
[jk]: https://jekyllrb.com/

현재 블로그는 [Github Page][ghpage]라는 서비스를 이용 중인데 별도의 동적 지원이 필요하지 않다면 무료로 제공되고, 무엇보다 Github와 완벽하게 연동되기 때문에 상당히 만족하면서 사용 중이다. [Tstory](https://www.tistory.com/)나 [Medium](https://medium.com/)은 직관적이고 간결한 서비스를 제공하는데 반해 Git Page는 개발자용이다 보니 자유도가 높다는 게 가장 큰 장점인 것 같다 ~~(github.io라는 주소가 간지난다는 것도...)~~.

[Github Page][ghpage]는 [Jekyll][jk]이라는 Ruby 기반의 엔진으로 작동하는 데 사실 지금까지 블로그만 생성해서 사용했을 뿐 내부에서 [Jekyll][jk]이 어떻게 작동되는지에 대해 거의 아는 게 없었다. 관련해서 [Mike Dane](https://www.youtube.com/channel/UCvmINlrza7JHB1zkIOuXEbw)이라는 Youtuber가 좋은 Tutorial을 작성하여 공부한 내용을 아래에 정리해본다. 19개의 약 5분 내외의 짧은 동영상으로 구성되어 있어 1시간 정도면 기본적인 내용을 모두 훑을 수 있다.


---

[Jekyll Official Document](https://jekyllrb.com/docs/)

아래 본문은 예시 문법 작성 시 jekyll이 자동 인식 및 작동하여 발생하는 오류를 회피하기 위해 `{}`를 `[]`로 표기하였다.

---

### 1 [Introduction](https://youtu.be/T1itpPvFWHI)

`jekyll` : Ruby 언어를 기반으로 구동
`gem` : Ruby Package Manager

### 2 [Mac Installation](https://youtu.be/WhrU9m82Wm8)

Mac의 경우, Ruby 및 Gem이 기본적으로 탑재되어 있다. 따라서 Version 확인 후 바로 `gem`을 통해 `jekyll`을 바로 설치하면 된다.

~~~Terminal
~ $ ruby -v						# Ruby 설치여부 및 버젼확인
~ $ gem -v						# Gem 설치여부 및 버젼확인
~ $ gem install bundler jekyll	# jekyll 엔진 설치
~ $ jekyll -v					# jekyll 설치여부 및 버젼확인
~~~

### 3 Windows Installation

### 4 [Creating a Site](https://youtu.be/pxua_1vyFck)

~~~Terminal
~ $ jekyll new my-awesome-site	# jekyll이 구동될 신규 블로그 폴더 생성 (minima theme이 기본테마)
~ $ cd my-awesome-site			# 생성된 블로그 폴더로 이동
~/my-awesome-site $ bundle exec jekyll serve	# Now browse to http://localhost:4000
~~~

* Command
	* `jekyll new BLOG_NAME` : 신규 폴더 및 기본 양식으로 블로그 생성
	* `bundle exec jekyll serve` : Local host에 블로그 페이지 생성 
		* 처음 혹은 _config.yml 변경 시에만 필요. 
		* http://127.0.0.1:4000/에서 조회 가능
* Folder
	* `_posts` : 작성된 Post를 저장하는 폴더. Markdown으로 작성 (.md)
	* `_site` : Website final version - 작성된 Markdown 등의 문서를 Jekyll에서 Compile 된 후 실제로 Web에서 호스트 될 최종 HTML 파일
* File
	* `_config.yml` : key value pair and parameter (세팅)
	* `Gemfile` : Jekyll dependency - Theme 등 (초기값은 minima 테마)
	* `index.md`	: HOME - 블로그 초기 페이지
	* `about.md`	: About 페이지

### 5 [Front Matter](https://youtu.be/ZtEbGztktvc)

* Front Matter
	* 개별 post의 가장 상단에 `---`로 정의된 페이지 속성 정보를 포함 (`.yml`)
	* 해당 정보로 jekyll이 개별 페이지 Rendering을 통해 HTML을 생성

~~~Markdown
---
layout : post 						# Templete 정보. 없으면 템플릿 미생성
title : "Welcome To Jekyll!"		# Post 제목. 없으면 파일 이름에서 추출
date : 2017-09-24 15:58:59 -0700 	# Post 일자. 없으면 파일 이름에서 추출
categories: jekyll update			
---
~~~

* Post URL 생성 : *categories/년/월/일/title with '-'.html*
	* ex. *https://jamescbjeon.github.io/investment/2022/01/21/book-perfect-SFP.html*
* `layout` 특성은 Customized 가능: 신규 생성 및 추후 변경 등 가능


### 6 [Writing Posts](https://youtu.be/gsYqPL9EFwQ)

* Post 작성 방법
	* ` _posts` 폴더에 새 파일 생성
		* `_posts` 내에 Subfolder 생성 및 개별 분류해도 동일하게 처리. 실제 웹페이지에서는 변화 없으므로 관리하기 용이
	* Markdown (`.md`)으로 작성
	* Naming convention : `yyyy-mm-dd-name-with-hipens.md`


### 7 [Working with Drafts](https://youtu.be/X8jXkW3k2Jg)

* `_drafts` : 완성 전 파일 보관 폴더
	* 가안 상태로 취급되어 Blog에서는 보이지 않음
	* 아직 작성 중이므로 정확한 작성 일자를 파일 이름에 포함할 필요 없음. 자동으로 현재 날짜로 취급
	* `Jekyll serve --draft` : draft post를 보함하여 rendering &rarr; Local host에서 작성 상태 확인 가능
	* 즉, `_draft` 폴더를 활용 해 Work-flow를 효율하게 유지 가능

### 8 [Creating Pages](https://youtu.be/1na-IWfv08M)

1. Post : `_post` 폴더에서 관리
2. Web page : 별도 폴더 관리
	* Front matter 설정 할 것 (ex. layout: "page")
	* 저장된 위치에 따라 localhost:4000/folder/name로 접근
	* 반드시 Markdown일 필요 없음. 모든 형태의 파일 가능.

### 9 [Permalinks](https://youtu.be/938jDG_YPdc)

Frontmatter - `permalink` : */지정이름/필요시서브폴더가능/포스트혹은파일이름*  
: 기존 URL convention이 아닌 사용자 지정 이름으로 URL 생성

~~~jekyll
/:categories		# 카테고리 이름으로 url 생성
/:year/month/day	# 년/월/일
/:title				# 제목
~~~

### 10 [Front Matter Defaults](https://youtu.be/CLCaJJ1zUHU)

~~~jekyll
_config.yml

defaults:
	-
		scope:
			path: ""
			type: "posts"	
		values:
				layout: "post"
				title: "...."
~~~

### 11 [Themes](https://youtu.be/NoRS2D-cyko)

Theme을 바꿔서 Blog 전체 모습을 손쉽게 변경 가능  
: rubygem.org &rarr; "Jekyll-theme" 검색

~~~jekyll
# "Gemfile" 내부에 필요 테마 추가
gem "jekyll-theme-yat"		# (예시) jekyll-theme-yat 테마 추가

# "_config.yml" 내부에 테마 적용
theme: jekyll-theme-yat		# (예시) jekyll-theme-yat 테마 적용

# Terminal 명령
~/my-blog $ bundle install				# Gemfile 내에 있는 테마 다운로드
~/my-blog $ bundle exec jekyll serve	# _config.yml이 업데이터 되었으므로 Re-rendering
~~~

> Error 발생 할 경우,  Front matter에 적용하는 Theme의 Layout 등이 제대로 반영되었나 확인 필요

### 12 [Layouts](https://youtu.be/bDQsGdCWv4I)

* `_layouts` 폴더 : 필요한 레이아웃 관리
	* Post, Page Layout &rarr; `post.html`, `page.html`과 같이 Layout 이름과 동일하게 생성 후 설정
	* Layout hierarchy를 통해 한 Layout에서 Front matter를 통해 다른 Layout을 사용할 수 있음
		* 즉 매번 Layout을 새로 생성할 필요 없이, Upper Layout이 정의되면 단계적으로 구체화 가능 (전체 통일성 유지 및 관리 유리)
	* `[[ contents ]]` : Post 내 전체 내용을 의미

### 13 [Variables](https://youtu.be/nLJBF2KiOZw)

> Jekyll에서 Post의 일부 항목, 특히 Front matter 대부분을 변수로 취급 가능하며 이를 통한 일괄 제어를 제공한다.  ([Official Document]( https://jekyllrb.com/docs/home/variables))

~~~jekyll
### Content
[[ content ]]		    # Post 본문

### Layout - [[ layout.attribute ]]
[[ layout.author ]]  	# 작성자

### Page - [[ page.attribute ]]
[[ page.title ]] 		# 페이지 Front matter에 정의된 제목

### Site
[[ site.title ]] 		# _config.yml에 정의된 Title 값
~~~

### 14 [Includes](https://youtu.be/HfcJeRby2a8)

* `_includes` : 모든 페이지에 공통으로 들어갈 만한 내용을 정의
	* (ex.) header.html &rarr; Header에 공통 적용될 내용을 정의

### 15 [Looping through Posts](https://youtu.be/6N1X5XffuUA)

> 변수를 활용하여 Post 전체에 Looping 가능하다

~~~
### Usage
[% for i in targets %]
	Loop
[% endfor %]

### (Example) home.html에서 전체 포스트 이름을 보여주려는 경우,
[% for post in site.posts %]		# Site 내 Post 전체를 Looping
	<li><a href="[[ post.url ]]">[[ post.title ]]</a></li>
[% endfor %]
~~~

### 16 [Conditionals](https://youtu.be/iNZBEki_x6o)

~~~
### Usage
[% if CONDITION %]		# 필요 시, 조건 사이에 "and"/"or" 사용 가능
	Command
[% elsif %]
	Command
[% else %]
	Command
[% end if %]

### (Example 1) 페이지 제목이 "My First Post"일 경우, 출력
[% if page.title == "My First Post" and %]
	This is the first post
[% endif %]

### (Example 2) 페이지와 포스트 URL이 동일할 경우, 링크 색깔을 붉게 변경
[% for post in site.posts %]
	<li><a style="[% if page.url == post.url %]color:red;[% endif %]" href="[[ post.url ]]">[[ post.title ]]</a></li>
[% endfor %]
~~~

### 17 [Data Files](https://youtu.be/M6b0KmLB-pM)

`_data` : 필요한 데이터 파일을 저장. 다른 파일에서 data 파일에 접근 가능

~~~
### Example. Site 내 _data 폴더의 people.yml 데이터 파일에서 For-loop를 통해 이름/직업을 출력
[[% for person in site.data.people %]]
	[[ person.name ]], [[ person.occupation ]] <br>
[[% endfor %]]
~~~

### 18 [Static Files](https://youtu.be/knWjmVlVpso)

`site.static_files` : Front matter가 필요 없는 파일. 예) javascript, css, pdf, jpeg 등

~~~
### Example. Site 내 Static file 전체를 loop하며 경로를 출력
[% for file in site.static_files %]
	[[ file.path ]] <br>
	[[ file.name ]] <br>
[% endfor %]
~~~

### 19 [Hosting on Github Pages](https://youtu.be/fqFjuX4VZmU)

* 설치 준비
	* git installed
	* github account
* 설치
	* github repository 생성
	* _config.yml : baseurl - "GITHUB REPO NAME"

~~~Terminal
~/my-blog $ git init
~/my-blog $ git checkout -b gh-pages
~/my-blog $ git status
~/my-blog $ git add .
~/my-blog $ git commit -m "COMMENT"
~/my-blog $ git remote add origin ADDRESS
~/my-blog $ git push origin gh-pages
~~~