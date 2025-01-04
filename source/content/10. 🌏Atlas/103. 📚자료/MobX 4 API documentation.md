---
date: 2025-01-02
---
# 주제: [[MobX]]
# Core API
These are the most important MobX API's.
> Understanding `observable`, `computed`, `reaction` and `action` is enough to master MobX and use it in your applications!

## 관찰 가능한 항목(observables) 만들기

### observable(value)
사용법
- `observable(value)`
- `@observable classProperty = value`

Observable values는 JS의 원시 값(primitive value), 참조 타입(references), 일반 객체(plain Objects), 클래스 인스턴스(class instances), 배열(arrays), 맵(maps)이 있다.

**Note**: `observable(value)`는 관찰 가능한 데이터 구조(배열, 맵 또는 관찰 가능한 객체)로 만들 수 있는 경우에만 성공하는 편의용 API다. 다른 모든 값의 경우 변환이 수행되지 않는다.

원하는 관측 가능한 유형(observable type)을 직접 만들 수도 있다.(아래 참조)

다음 변환 규칙들이 적용되지만 decorators를 사용하여 세부적으로 조정할 수 있다.
1. **값이 ES6 맵의 인스턴스인 경우** 새 관찰 가능한(observable) 맵이 반환된다. 관찰 가능한 맵은 특정 항목의 변경뿐만 아니라 항목의 추가 또는 제거에도 반응하고 싶을 때 매우 유용하다.
2. **값이 배열인 경우** 새 관찰 가능한 배열이 반환된다.
3. **값이 프로토타입이 없는 객체이거나 프로토타입이 `Object.prototype`인 경우** 객체가 복제되고 모든 현재 프로퍼티(properties)가 관찰 가능하게 된다.
4. **값이 프로토타입, JS 원시 값, 함수가 있는 객체인 경우** 값이 변경되지 않는다. 박스형(Boxed) Observable이 필요한 경우 다음 중 하나를 수행하면 된다:
	- `observable.box(value)`를 명시적으로 호출한다.
		- `import { observable} from 'mobx';`
		- `const boxedValue = observable.box(42);`
		- 원시 값은 Boxed Observable로 변환
	- 클래스 정의에 `@observable`을 사용한다.
		- `import { observable } from 'mobx';`
		- `class Store {`
		- `  @observable value = 42;`
		- `}`
		- 클래스 속성을 observable로 만듦
	- `decorate()`를 호출한다.
		- `import { observable, decorate } from 'mobx';`
		- `class Store {`
		- `  valuew = 42;`
		- `}`
		- `decorate(Store, {`
		- `  value: observable`
		- `});`
		- decorate를 사용하여 클래스 속성을 observable로 만듦
	- `extendObservable()`을 사용하여 클래스 정의에 프로퍼티를 도입한다.
		- `import { extendObservable } from 'mobx';`
		- `class Store {`
		- `  constructor() {`
		- `    extendObservable(this, {`
		- `      value: 42`
		- `    });`
		- `  }`
		- `}`
		- extendObservable을 사용하여 클래스 속성을 observable로 만듦


MobX는 자동적으로 관찰 가능한 프로토타입이 있는 객체를 만들지 않는다. 이는 생성자(constructor) 함수의 책임이기 때문이다. 대신 생성자 함수에 `extendObservable`을 사용하거나 클래스 정의에 `@observable`을 사용하면 된다.

이러한 규칙들은 언뜻 보기엔 복잡해보일 수 잇지만 실제로 매우 직관적으로 작동하는 것을 알 수 있을 것이다

**몇 가지 참고 사항**
- `@observable` 데코레이터를 사용하려면 트랜스파일러(babel or typescript)에서 데코레이터를 활성화 해야 한다.
- 기본적으로 데이터 구조를 관찰 가능으로 설정하면(감염성이 있다.is infective) 데이터 구조에 포함되어 있거나 향후 데이터 구조에 포함될 모든 값에 `observable`이 자동으로 적용된다.
- [MobX 4 이하] 동적으로 키가 지정된 객체를 만들려면 항상 맵을 사용해야 한다! 처음에는 객체의기존 프로퍼티만 관찰할 수 있게 되지만, 새로운 프로퍼티들은  `extendObservable`을 사용하여 추가할 수 있다.

### @observable property = value
`observable`은 프로퍼티 데코레이터로도 사용될 수 있다. <br>데코레이터가 활성화되어 있어야 하며 `extendObservable(this, { property: value })`를 쉽게 사용하게 해준다(syntactic sugar).

### Decorators
`observable`, `extendObservable` 그리고 `observable.object`로 정의된 프로퍼티들의 관찰 가능한 정도를 미세조정하기위해 데코레이터를 사용한다. 또한 특정 프로퍼티에 대한 자동 변환 규칙을 제어할 수도 있다.

다음의 데코레이터들이 가능하다:
- `observable.deep`: 모든 observable에서 사용되는 기본 데코레이터다. 할당된 값(any assigned, non-primitive value)이 아직 관찰 가능한 값이 아닌 경우 관찰 가능한 값으로 변환한다.
- `observable.ref`: 관찰 가능한 자동 변환을 비활성화하고 관찰 가능한 참조만 만든다.
- `observable.shallow`: 컬렉션과 함께만 사용할 수 있다. 할당된 컬렉션을 딥(deep)대신 얕게 관찰 가능한 컬렉션으로 변환한다. 즉, 컬렉션 내부의 값은 자동으로 관측 가능한 값이 되지 않는다.
- 