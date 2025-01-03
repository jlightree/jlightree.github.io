MobX는 리액트 컴퍼넌트의 상태를 관리하기 위해 사용하는 상태 관리 컨테이너다.
# 기반 지식
## state 관리 개요
- 클래스 기반의 컴포넌트는 state 객체를 이용해 변경 가능한 데이터를 관리한다.
	- 특정 이벤트에 따라 데이터를 변경하고 변경에 따라 컴포넌트의 UI가 새롭게 렌더링된다.
- 사용자 UI는 다수의 컴포년트를 통해 표현되며 각 컴포년트가 state를 관리할 경우 데이터 관리 및 제어가 어렵다.
- 각각의 컴포년트에서 특정 데이터의 공유가 필요한 경우 이 데이터를 참조하거나 변경할 때 제약이 발생한다.
- 공통의 데이터 관리 영역(store)을 두고 이를 통해 state를 관리하면 컴포년트 간 데이터 공유가 가능하다.
- ![[Screenshot_20241227_103634_YouTube.jpg]]

## Flux
- Flux는 React를 이용한 UI 구성에서 데이터의 흐름을 관리하는 어플리케이션 아키텍처
- MVC 구조의 데이터 흐름은 View와 Model 사이에 양방향 데이터 이동이 가능
- MVC 구조는 View가 많아질수록 데이터의 흐름과 관리가 어려움
- React는 단방향 데이터 흐름(Model -> View)만 가능하기 때문에 MVC 아키텍처는 미적용
- 단방향 데이터 흐름은 구조를 단순화할 수 있으며 데이터의 이동 또한 명확하게 확인 가능
- ![[Screenshot_20241227_113108_YouTube.jpg]]
- Flux는 단방향 데이터 흐름을 보완하기 위해 개발된 아키텍처이며 View로 분산된 state를 통합 관리한다.
- Flux 아키텍처는 Action, Store, Dispatcher, View로 구성한다.
- View 각각의 state는 Store를 이용해 통합 관리되며, Store의 데이터는 Action을 이용해 제어한다.
- Store에서 제어하는 state는 곧 연결된 View의 state와 다름없으며 Store의 state가 변경되면 View도 갱신된다.
- ![[Screenshot_20241227_130918_YouTube.jpg]]

# MobX 개요
- MobX도 Flux와 마찬가지로 클라이언트 사이드에서 state를 관리하기 위해 사용하는 라이브러리다.
- MobX를 이용하면 컴포넌트의 state를 별도의 영역(Store)에서 관리하고 각 컴포넌트는 이에 접근(inject사용)할 수 있다.
- MobX를 적용하기 위해서는 mobx.js 라이브러리와 mobx-react.js 라이브러리가 필요하다.
	- mobx: 실제로 Store를 관리하는 라이브러리
	- mobx-react: MobX를 react에 적용하는 라이브러리
- MobX는 다수의 store를 관리할 수 있으며, 관리하는 데이터는 특정 데이터의 형태(Observable)로 관리한다.
- ![[Screenshot_20241227_131427_YouTube.jpg]]
- MobX가 제공하는 대표적인 API는 observable, action, observer, computed가 있다.
	- action: observable 데이터를 변경할 때 사용
- MobX 라이브러리는 TypeScript가 적용되어 있으며 API의 사용은 데코레이터(@)를 사용하는 것이 일반적이다
- @observable API는 Store에서 관리하고자 하는 state 데이터를 의미하며 Observable 객체를 통해 관리된다.
- @observer API는 @observable API로 관리되는 state를 참조하는 React 컴포넌트에 적용한다.
- ![[Screenshot_20241227_132115_YouTube.jpg]]

## 실습
- src에 Store 폴더(패키지)를 만들어서 State를 관리하는 class를 만들어준다.
### state만들기
```Javascript
import { observable } from 'mobx';

class CounterStore {

	// 자바스크립트의 정식 문법으로 등록되지 않았으므로 Babel과 같은 트랜스파일러를 통해 코드를 변환해야 한다.
	@observable
	_count = 5;_
}

// export default CounterStore; // 이렇게 하면 사용하는 쪽에서 생성해야 함
export default new CounterStore();
```

### Provider
```JavaScript
import { Provider } from 'mobx-react';
import CounterStore from './store/CounterStore';

ReactDOM.render(
	// MobX와 React를 연결해ㅓ props 형태로 제공한다.
	<Provider counterStore = {CounterStore}>
		<App />
	</Provider>,
	document.getElementById('root')
);
```

### @inject
```javascript
import { inject } from 'mobx-react';

// Provider로 제공되는 Store들 중 counterStore를 props에 주입해준다.
@inject('counterStore')
class CounterComponent extends Component {
	render() {
		const { counterStore } = this.props;
	}
}
```
- MobX는 다수의 store를 구성하는 것이 가능하며 @inject를 이용해 해당 @observer 컴포넌트의 store를 주입한다.
- 주입된 store 객체들은 props에서 꺼내 사용한다.

### @action, @makeObservable
```javascript
import { observable, action, makeObservable } from 'mobx';

class CounterStore {
	constructor() {
		// MobX 버전 6이 되면서 데코레이터 지원을 빼면서 해당 내용을 선언해줘야 한다.
		makeObservable(this);
	}

	@observable
	_count = 5; // JavaScript에선 관례적으로 private한 데이터 or 메소드는 앞에 언더바를 붙여서 표시한다.

	// ECMA Script6(ES 2015)에서 get 메소드는 프로퍼티처럼 사용한다.(counterStore.count 이런 식으로 사용 가능)
	get count() {
		return this._count;
	}

	@action
	increment() {
		this._count ++;
	}

	@action
	decrement() {
		this._count --;
	}
}

export default new CounterStore();
```
- observable한 데이터를 변경할 때는 action을 이용해서 변경하는 것이 기본이다.
- 관찰 대상 데이터 즉, observable state의 값을 변경하는 메서드에 적용한다.
- @action을 붙이지 않아도 동작엔 이상이 없지만 한 메소드에서여러 state를 변경할 때 @action이 한번만 렌더링이 일어나게 한다.(transaction으로 감싸서, 함수가 완료될 때(state들의 변경이 완료될 때)까지 중간 상태가 외부에 노출되지 않도록 한다.)
- state에 대한 단순 조회와 같은 메서드에 적용하는 것은 의미가 없다.

### @observer
```JavaScript
import { inject, observer } from 'mobx-react';

@inject('counterStore')
@observer // observable한 데이터를 주시하고 있음을 명시해주는 API
class CounterComponent extends Component {

}
```
- store를 통해서 state를 관리하는 React.Component에 적용한다.
- @observer가 적용된 React.Component는 관련 observable state가 변경되면 렌더링을 수행한다.
	- @autorun + render

### @computed
- get 메서드에 일반적으로 적용하거나 Model 객체간 전환 시점에 적용한다.
- @computed가 적용된 메서드를 수행할 때 해당 observable state의 변화가 없을 경우 내부 로직을 생략한다.(캐싱을 통한 성능 최적화)

### 기타 API
- @autorun
	- 특정 state가 변경되었을 때 지정된 함수를 자동으로 실행한다.
- @transaction

# MobX의 적용
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