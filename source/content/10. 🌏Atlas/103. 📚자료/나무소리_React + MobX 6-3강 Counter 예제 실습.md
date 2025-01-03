---
date: 2024-12-27
---
# 주제: [[MobX]]
## 실습
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

### @observer
```JavaScript
import { inject, observer } from 'mobx-react';

@inject('counterStore')
@observer // observable한 데이터를 주시하고 있음을 명시해주는 API
class CounterComponent extends Component {

}
```