---
date: 2025-01-02
---
# 주제: [[MobX]]
## MobX의 적용
- React와 MobX를 통한 UI 구성은 다음과 같은 패키지의 구성을 갖는다.
	- container: React Component로 구성하며 store와 React Component를 연결하는 역할을 담당한다.
	- view: 순수 React Component로 구성하며 container에 포함된다.
	- repository(or api): 서버와 통신을 담당하는 클래스로 구성한다.
	- store: 전역 state를 관리하는 Store 클래스로 구성한다.
	- model: 서버의 model과 view model의 전환을 담당한다.
- container로 정의한 React 컴포넌트의 state는 store를 통해 관리한다.
	- view보다 큰 개념인 container가 store와 @inject를 통해 연결되어 state를 받아 view로 props를 통해 내려준다.
- store는 @action 메소드를 포함하며 이 메소드 호출을 통해 state를 제어한다.
- store의 state 데이터에 변경이 일어나면 해당 state와 연결된 React Component는 다시 렌더링된다.
- api는 서버와 통신을 담당하며 axios.js와 같은 서드-파티 라이브러리(Third-party Lib.)를 사용한다.
- ![[Screenshot_20250102_081646_YouTube.jpg]]
## 예제 폴더 구조
- src
	- containers
		- SearchbarContainer.js
		- TodoEditFormContainer.js
		- TodoListContainer.js
	- stores
	- views
		- TodoEditFormView.js
		- TodoListView.js
- ![[Screenshot_20250102_082919_YouTube.jpg]]