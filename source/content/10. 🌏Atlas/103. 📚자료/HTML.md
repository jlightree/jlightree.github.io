웹 페이지를 위한 코드

# 확장자
- 웹 페이지의 확장자는 html이다.

# 태그
- `<!doctype html>`: 이 웹 페이지가 HTML로 만들어졌음을 나타내는 관용적인 태그
 - `<html></html>`: `<head>`와 `<body>`를 감싸는 태그
- `<head></head>`: 본문을 설명하는 태그
- `<title></title>`: 웹 브라우저의 탭에 태그 안의 내용을 보여준다.
	- 검색엔진이 웹 페이지를 분석할 때 가장 중요하게 여기는 태그다.
- `<meta>`: 본문을 설명하는 태그 중 하나
	- `<meta chaset="utf-8">`
		- 코드가 utf-8로 쓰였음을 나타낸다.
- `<body></body>`: 본문이 들어가는 태그
- `<a></a>`:링크
	- anchor의 첫글자 a를 땄다.
	- `<a href="https://www.w3.org/TR/html5/" target="_blank" title="html5 specification">Hypertext Markup Language (HTML)</a>`
		- href는 <strong>H</strong>yperText <strong>Ref</strong>erence의 약자다.
		- `target="_blank"`는 링크를 클릭햇을 때 새 창에서 페이지가 열리게 하는 속성이다.
		- title은 링크가 담고 있는 내용을 툴팁으로 보여준다.
- `<strong></strong>`: 굵게
- `<u></u>`: 밑줄
- `<h1></h1>`: 제목
- `<br>`: 줄바꿈
- `<p></p>`: 단락
	- `<p style="margine-top:45px"></p>`: 단락과 단락의 고정된 간격을 내가원하는 대로 바꾸기 위해 CSS를 적용한다.
- `<img>`: 이미지
	- [[#속성(attribute)]]사용
- `<ul></ul>`: 목록
	- `<li></li>`를 자식 태그로 가진다.
- `<ol></ol>`: 순번
	- `<li></li>`를 자식 태그로 가진다.
## 속성(attribute)
- 태그의 심화 문법
- src
	- source의 줄임말
	- <img src="https://s3-ap-northeast-2.amazonaws.com/opentutorials-user-file/module/3135/7648.png">
	- `<img src="https://s3-ap-northeast-2.amazonaws.com/opentutorials-user-file/module/3135/7648.png">`
	- img 태그에 src를 붙여서 속성을 부여해줬다.
# 기능
- 검색 엔진은 웹 페이지를 분석하여 사용자가 검색했을 때 검색 결과를 보여준다.
	- <h3>Title</h3>
	- `<h3>Title</h3>`
	- <strong><span style="font-size:22px; color:#E5BF7F">Title</span></strong>
	- `<strong><span style="font-size:22px; color:#E5BF7F">Title</span></strong>`
	- 위 두 개의 Title은 같아보이지만 코드를 봤을 때는 제목 태그와 시각적인 장식을 한 태그로 나뉜다.
	- => HTML을 의미에 맞게 잘 사용하는 것은 비즈니스에 있어 중요하다.
	- 또한 시각장애인들은 스크린리더와 같은 프로그램을 이용해 정보를 청각화해서 접하므로 그런 사용자들에게도 도움이 된다.
# 다른 언어와의 관계
- HTML은 접착제같은 것이다.
- HTML이 CSS와 JavaScript를 가져온다.
- [[JavaScript]]를 사용하는 이유는 HTML과 상호작용하기 위함이다.
	- HTML의 Element들을 JavaScript를 통해 변경하고, 읽을 수 있다.
	- 이미 브라우저를 통해 HTML은 JavaScript와 연결되어있다.
## document
- 브라우저에 이미 존재하는 object
- HTML을 가리키는 객체
- JavaScript는 document를 이용해 HTML코드와 HTML Element에 접근할 수 있다.