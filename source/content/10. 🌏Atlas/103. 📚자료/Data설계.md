1. Data화 대상
2. Owner 특정
3. Task Leveling
4. Grouping
	- Schema(Owner)
	- Transactions Define(App 설계 시작)

### Task Leveling
- Process - Sub-Porcess - Task - Step(Activity) 순으로 Leveling을 해야한다.
	- Task를 잘 정하면 그 위인 Process들과 아래인 Step을 수월하게 정할 수 있다.
	- Task를 이해하기 위해 Transaction 개념을 알아야 한다.

### Transaction
- Start - End까지 개입이 불가한 단위
- ATM기기 예시
	- 카드를 ATM기기에 넣으면 메뉴가 나오기까지가 한 Transaction이다.
- 프로그램이 처리하는 단위

### 대출 과정에 대해 Task짜기
ㅁ Task#1: 대출 신청(Owner: 나)
 |
ㅁ Task#2: 심사(Owner: 은행)
 |(승인일 경우)-------------------------------ㄱ(거절일 경우)
ㅁ Task#3: 추가 서류 제출 및 서명(Owner: 나)    ㅁ Task#4: 거절에 대한 문자 안내(Owner: 은행)

위의 모습처럼 한 Owner단위로 Task를 구성해야하므로 Owner가 변경될 때마다 Task가 달라진다.

### Step
Owner가 달라질 때마다 Task가 추가됐으므로 한 Task하위의 Step들은 모두 Owner가 같다.