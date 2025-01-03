# document
- HTML이 제공하는 object
![[HTML#document]]
## 함수
### getElementById("[id]")
- document에서 id에 해당하는 Element를 가져온다.
### querySelector()
- element를 CSS 방식으로 검색할 수 있다.
```HTML
<div class="hello">
	<h1>Grab me!</h1>
</div>
```
```JS
// App.js
const title = document.querySelector(".hello h1")
```
- 같은 내용이 반복해서 있다면 처음의 것이 나온다.
- id의 경우 `#`을 붙여주면 된다.: `#hello`
### querySelectorAll()
- 여러개를 찾고싶은 경우 사용한다.