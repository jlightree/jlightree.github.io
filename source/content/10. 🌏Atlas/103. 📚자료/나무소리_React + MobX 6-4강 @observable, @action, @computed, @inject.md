---
date: 2024-12-31
---
# 주제: [[MobX]]
## MobX 개요
###  @action
- 관찰 대상 데이터 즉, observable state의 값을 변경하는 메서드에 적용한다.
- @action을 붙이지 않아도 동작엔 이상이 없지만 한 메소드에서여러 state를 변경할 때 @action이 한번만 렌더링이 일어나게 한다.(transaction으로 감싸서, 함수가 완료될 때(state들의 변경이 완료될 때)까지 중간 상태가 외부에 노출되지 않도록 한다.)
- state에 대한 단순 조회와 같은 메서드에 적용하는 것은 의미가 없다.

### @computed
- get 메서드에 일반적으로 적용하거나 Model 객체간 전환 시점에 적용한다.
- @computed가 적용된 메서드를 수행할 때 해당 observable state의 변화가 없을 경우 내부 로직을 생략한다.(캐싱을 통한 성능 최적화)

### @observer
- store를 통해서 state를 관리하는 React.Component에 적용한다.
- @observer가 적용된 React.Component는 관련 observable state가 변경되면 렌더링을 수행한다.
	- @autorun + render

### @inject
- MobX는 다수의 store를 구성하는 것이 가능하며 @inject를 이용해 해당 @observer 컴포넌트의 store를 주입한다.
- 주입된 store 객체들은 props에서 꺼내 사용한다.

### 기타 API
- @autorun
	- 특정 state가 변경되었을 때 지정된 함수를 자동으로 실행한다.
- @transaction