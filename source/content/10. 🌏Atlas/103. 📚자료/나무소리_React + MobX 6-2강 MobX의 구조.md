---
date: 2024-12-27
---
# 주제: [[MobX]]
## MobX 개요
- MobX도 Flux와 마찬가지로 클라이언트 사이드에서 state를 관리하기 위해 사용하는 라이브러리다.
- MobX를 이용하면 컴포넌트의 state를 별도의 영역에서 관리하고 각 컴포넌트는 이에 접근할 수 있다.
- MobX를 적용하기 위해서는 mobx.js 라이브러리와 mobx-react.js 라이브러리가 필요하다.
- MobX는 다수의 store를 관리할 수 있으며, 관리하는 데이터는 특정 데이터의 형태(Observable)로 관리한다.
- ![[Screenshot_20241227_131427_YouTube.jpg]]
- MobX가 제공하는 대표적인 API는 observable, action, observer, computed가 있다.
	- mobx: 실제로 Store를 관리하는 라이브러리
		- action: observable 데이터를 변경할 때 사용
	- mobx-react: MobX를 react에 적용하는 라이브러리
- MobX 라이브러리는 TypeScript가 적용되어 있으며 API의 사용은 데코레이터(@)를 사용하는 것이 일반적이다
- @observable API는 store에서 관리하고자 하는 state 데이터를 의미하며 Observable 객체를 통해 관리된다.
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

### inject
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