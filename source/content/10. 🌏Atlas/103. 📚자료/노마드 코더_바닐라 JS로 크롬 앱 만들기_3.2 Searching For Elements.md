---
date: 2024-11-11
---
# 주제: [[JavaScript]]
지난 시간에 `document.getElementById`를 배웠지만 대부분 class를 사용하거나 class와 id를 사용한다.
# querySelector()
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
