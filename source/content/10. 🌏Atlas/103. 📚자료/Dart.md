# Dart의 특징
- 객체 지향 언어
- 구글에서 만듬
- UI에 최적화
- 생산적인 개발환경
- 모든 플랫폼에서 빠름
- 여러 컴파일러
	- Dart Web
		- Dart로 쓴 코드를 javascript로 변환
	- Dart Native
		- Dart로 쓴 코드를 여러 CPU의 아키텍쳐에 맞게 변환
		- ARM32
		- ARM64(대부분의 모바일 기기)
		- x86_64(데스크탑)
		- <span style="color:green">JIT(just-in-time)</span>
			- Dart VM 사용
				- 코드의 결과를 바로 화면에 보여줌
		- <span style="color:green">AOT(ahead-of-time)</span>
			- 컴파일시 아키텍처를 지정
			- 해당하는 아키텍처에 대한 바이너리(machine code)로 컴파일하여 바이너리 배포
			- 단점 
				- UI를 개발시엔 느림
				- 뭔가 하나를 바꿔도 그 바꾼 것에 대한 결과를 위해 처음부터 끝까지 컴파일 해야 함
		- ⇒ 개발할땐 JIT, 배포할 땐 AOT
	- => IOS, Android, Windows, Linux, Mac 등등으로 컴파일 가능
- null safety
	- 안전한 프로그램을 빌드할 때 중요
- flutter가 Dart를 선택한 이유
	1. JIT 컴파일과 AOT 컴파일이 둘 다 있음
		- ⇒ 모바일 개발에 아주 좋은 언어(빠른 피드백, 빠른 최종 앱)
	2. Dart와 Flutter 둘 다 구글에서 만듬
		- ⇒ Flutter를 위해 Dart 최적화 가능

# 문법적 특징
- 반드시 main 함수를 써줘야 함
	- Dart는 자동적으로 main 함수를 찾음
	- 실제로 작성할 코드의 대부분은 main 내부에 있음
	- class나 type같은건 main 밖에 만듬
- 모든 줄 뒤에 ;(세미콜론)을 붙여줘야 함
	- 일부러 ;(세미콜론)을 안 쓰는 경우도 있으므로 <span style="background:#d3f8b6; color:black">자동 formatter가 ;(세미콜론)을 붙여주지 않음</span>
## 변수
### var: ==기본적인 변수 선언1==
- <span style="color:blue">var (변수명) = (데이터)</span>
- `var name = '승훈’`
- 컴파일러가 변수의 타입을 추론하므로 <span style="background:#d3f8b6; color:black">함수나 메소드 내부에 지역 변수를 선언하는 대부분의 상황에서 `var` 사용 권장</span>
- 변수를 업데이트할 때는 기존 타입에 맞춰서 업데이트 해줘야 함
### 명시적으로 데이터 타입 지정: ==기본적인 변수 선언2==
- <span style="color:blue">(타입) (변수명) = (데이터)</span>
- `String name = '승훈‘`
- <span style="background:#d3f8b6; color:black">class에서 변수나 property를 선언할 때 사용 권장</span>
### final: ==수정할 수 없는 변수==
- <span style="color:blue">final (변수명) = (데이터)</span>
- 값을 재할당하지 못하는 변수를 만듬
- <span style="background:#d3f8b6; color:black">런타임중에 할당 가능</span>(사용자가 앱을 실행하면서 변수를 만들 수 있음)
```dart
void main() {
	final name = '승훈';
	// 더 확실히 하고 싶으면 변수형을 final 뒤에 써줘도 되는데 권장사항은 아님
	final String name2 = '이드'
}
```
### const: ==수정할 수 없는 변수==
- <span style="color:blue">const (변수명) = (데이터)</span>
- compile-time constant를 만듬
- final과 같이 작동하며 추가적으로 <span style="background:#d3f8b6; color:black">compile-time에 값을  알고 있어야 함</span>(앱스토어에 앱을 올리기 전에 알고 있는 값)
- 사용자가 화면에 입력하는 값이거나 API로부터 받아오는 값이면 const를 쓸 수 없고 final이나 var를 사용해야 함
### dynamic: ==여러 데이터 타입 할당==
- <span style="color:blue">dynamic (변수명) = (데이터)</span>
- 여러가지 데이터 타입을 가질 수 있는 변수에 쓰는 키워드
- dynamic이 필요한 경우
	- 변수가 어떤 타입인지 알기 어려운 경우
		- 특히 flutter나 json이랑 함께 작업하면 자주 발견 가능
	- dynamic으로 돌아가는게 더 유용할 경우
- 사용되는게 추천되진 않지만 때때로 유용
- <span style="background:#d3f8b6; color:black">dynamic 직접 명시</span>
```dart
void main() {
	dynamic name;
	name = '승훈';
	name = 12;
	name = true;
}
```
- 변수 선언시 데이터를 할당하지 않으면 <span style="background:#d3f8b6; color:black">변수의 타입이 dynamic이 되어 여러 데이터 타입을 선언 가능</span>
```dart
void main() {
	var name;
	name = '승훈';
	name = 12;
	name = true;
}
```
- Dart가 dynamic을 통해 변수의 기능을 제한함
```dart
void main() {
	dynamic name;
	if(name is String) {
		name.//String에 관한 옵션 제공
	}
	name.//dynamic에 관한 몇가지의 옵션만 제공
}
```
### late: ==추후 변수 사용시 데이터 할당==(설명을 수정해야할수도)
- <span style="color:blue">late (변수 선언 키워드) (변수명) = (데이터)</span>
- 해당 변수가 사용 될 때 변수가 정의되어 있는지확인
- flutter로 API에서 데이터를 가져올 때 유용
- (필요한 데이터가 아직 없을 수 있으므로) 데이터 없이 변수를 만듬
```dart
void main() {
	late final String name;
	// do something, maybe go to API
	name = '승훈';
}
```
- 값을 넣기 전에 변수를 사용하려 하면 Dart가 사용하면 안된다고 알려줌(null safety와 유사)
```dart
void main() {
	late final String name;
	// do something, maybe go to API
	print(name); // 에러
}
```
### null safety: ==잘못된 상태의 변수 참조 보호==
- Dart의 모든 변수는 non-nullable
- `String name = null; // null값 참조 불가능`
- [[Dart#null safety 사용|null safety]]
	- `String? name = null;`
- [[Dart#null safety를 사용하지 않은 경우|null 참조시]]엔 런타임 에러(사용자가 앱을 사용하는 중에 뜨는 에러)가 뜸
- [[Dart#null safety 사용|null을 참조]]하기 위해선 어떤 변수, 데이터가 null이 될 수 있음을 명시해줘야 함
#### null safety를 사용하지 않은 경우
```dart
// Without null safety:
bool isEmpty(String string) => string.length == 0;

main() {
	isEmpty(null);
}
```
NoSuchMethodError가 뜸

#### null safety 사용
Dart에서는 어떤 변수가 null이 될 수 있음을 정확히 표시해야 함
```dart
void main() {
	String? name = '승훈';
	name = null;
	if (name != null) {
		nico.isNotEmpty;
	}
	// 단축 문법
	name?.isNotEmpty;
}
```

## Class
flutter에서는 class가 정말 중요
다른 언어와의 차이도 잘 숙지
```dart
class Player {
	final String name = 'ead'; // 값을 변경하지 못하게 할 때는 final
	int xp = 1500;
void sayHello() {
	print("Hi my name is $name");// this.name도 동작은 하지만 안 해도 됨
}
}

void main() {
	var player = Player();// new Player()를 쓸 수는 있지만 안 해도 됨
	print(player.xp); // 1500
	player.xp = 100
	print(player.xp); // 100

	player.sayHello(); // 'Hi my name is ead'
}
```

### Constructor
- argument로 class의 변수들에 대한 값을 할당
1. late를 통해 변수들의 값을 나중에 받아올 것임을 인지시킴
2. class 이름을 그대로 써서 constructor를 만듬
```dart
class Player {
	late final String name;
	late int xp;

	Player(String name, int xp) {
		this.name = name;
		this.xp = xp;
	}

	void sayHello() {
		print("Hi my name is $name");
	}
}

void main() {
	var player = Player('ead', 1500);
	player.sayHello(); // 'Hi my name is ead'
	var player2 = Player('vic', 1500);
	player2.sayHello(); // 'Hi my name is vic'
}
```
- 더 간결하게 하는 법
```dart
class Player {
	final String name;
	int xp;

	Player(this.name, this.xp);

	void sayHello() {
		print("Hi my name is $name");
	}
}
```
#### Named Constructor Parameters
- [[#Parameter]]의 [[#Named Parameters]]와 같음
```dart
class Player {
	final String name;
	int xp;
	String team;
	int age;

	Player({
		required this.name,
		required this.xp,
		required this.team,
		required this.age
	});

	void sayHello() {
		print("Hi my name is $name");
	}
}

void main() {
	var player = Player(
		name: "ead",
		xp: 1500,
		team: "blue",
		age: 32,
	)
}
```
#### Named Constructors
새로운 (Named) Constructor를 만들고 콘론을 통해 Player 객체를 초기화
```dart
class Player {
	final String name;
	int xp, age;
	String team;

	Player({
		required this.name,
		required this.xp,
		required this.team,
		required this.age
	});
// createBluePlayer라는 새로운 메서드
// 콜론 뒤에서부터 Player 클래스를 초기화
	Player.createBluePlayer({
		required String name,
		required int age,
	}) : this.age = age,
		this.name = name,
		this.team = 'blue',
		this.xp = 0;

	void sayHello() {
		print("Hi my name is $name");
	}
}

void main() {
	var player = Player.createBluePlayer(
		name: "ead",
		age: 32,
	)
}
```
##### 실사례
API로부터 여러 Player가 들어있는 목록을 받는 상황
```dart
class Player {
	final String name;
	int xp;
	String team;

	Player.fromJson(Map<String, dynamic> playerJson) :
		name = playerJson['name'],
		xp = playerJson['xp'],
		team = playerJson['team'];

	void sayHello() {
		print('Hi my name is $name');
	}
}

void main() {
	var apiData = [
		{
			'name': 'ead',
			'team': 'red',
			'xp': 0,
		},
		{
			'name': 'vic',
			'team': 'red',
			'xp': 0,
		},
		{
			'name': 'ted',
			'team': 'red',
			'xp': 0,
		},
	];

	apiData.forEach((playerJson) {
		var player = playerJson.fromJson(playerJson);
		player.sayHello();
	})
}
```
### Abstract Class(추상화 클래스)
- 객체 생성 불가
- 다른 클래스들이 직접 구현해야하는 메소드들을 모아놓은 일종의 청사진
- 메소드의 이름과 반환 타입만 정의 가능
- 특정 메소드를 구현하도록 강제
```dart
abstract class Human {
	void walk();
}

enum Team { red, blue }

class Player extends Human {
	String name;
	int xp;
	Team team;

	Player({
		required this.name,
		required this.xp,
		required this.team,
	});

	void walk() {
		print('I\'m walking');
	}

	void sayHello() {
		print("Hi my name is $name");
	}
}
	var vic = Player(name: 'vic', xp: 1200, team: Team.red)
	..name = 'test'
	..xp = 1234
	..team = Team.blue;
}
```
### Inheritance(상속)
[[노마드 코더_Dart 시작하기 4.8 Inheritance|원본]]
- super 키워드를 통해 (확장을 한) 부모 클래스와 상호작용(프로퍼티 접근, 메소드 호출)
```dart
class Human {
	final String name;
	Human(required this.name);
	void sayHello() {
		print("Hi my name is $name");
	}
}

enum Team { blue, red }

class Player extends Human {
	final Team team;

	Player({
		required this.team,
		required String name,
	}) : super(name: name);

	@override
	void sayHello() {
		super.sayHello();
		print('and I play for ${team});
	}
}

void main() {
	var player = Player(team: Teanred, name: 'ead);
}
```
### Mixins
[[노마드 코더_Dart 시작하기 4.9 Mixins|원본]]
- 생성자가 없는 클래스
- 내부의 프로퍼티와 메소드들을 가져옴
```dart
class Strong {
	final double strengthLevel = 99.99;
}
class QuickRunner {
	void runQuick() {
		print("Run!!");
	}
}

class Tall {
	final double height = 1.99;
}

enum Team { blue, red }

class Player with Strong, QuickRunner, Tall {
	final Team team;
}

class Horse with Strong, QuickRunner {}
```
## Dart의 자료형
- 대부분의 자료형들(function도 포함)은 object이다.
	- ⇒ 진정한 객체지향 언어로 불리는 이유
### String 
- 작은 따옴표('), 큰 따옴표(") 둘 다 가능
- 작은 따옴표내에서 작은 따옴표가 보여야할 때는 `￦'`사용
- [[#String Interpolation text에 변수를 추가|String Interpolation]] 기능으로 text에 변수 추가 가능
### bool
- true
- false
### int
### double
### num
- 정수형, 실수형 다 가능
- [[#int]], [[#double]] class들이 num을 상속
### List
- Flutter에서 유용
- `var numbers = [1, 2, 3, 4];`
- `List<int> numbers = [1, 2, 3, 4];`
- 몇몇 IDE에서는 List의 끝 요소 뒤에 ','를 붙여주면 자동으로 여러 줄로 포매팅
[[#collection If]], [[#collection For]] 지원
### Map
- key와 value에 어떤 것도 명시 가능
- JavaScript나 TypeScript의 object, phthon의 dictionary같은 것
```dart
void main() {
	var player = {
		'name': 'ead',
		'xp': 19.99,
		'superPower': false,
	}
}
```
- => Map<String, Object>: key(String)와 value(Object)로 이뤄져있음

- 데이터타입 직접 선언
```dart
void main() {
	Map<int, bool> player = {
		1: true,
		2: false,
	}
}
```

### set
List와 다른 점은 Set에 속한 모든 아이템들은 유니크함(값을 하나씩만 가짐)
sequence(순서가 있음)
중괄호 사용시 Set 자동 사용
```dart
void main() {
	var numbers = {1, 2, 3, 4};
}
```

# Dart의 기능
## String Interpolation: text에 변수를 추가
- (작은 따옴표나 큰 따옴표 내에서)<font color="blue">'$(변수명)'</font>
- <font color="blue">'${(변수명) + 계산}'</font>
```dart
void main() {
	var name = '승훈';
	var age = 30;
	var greeting = 'Hello everyone, my name is $name, I\'m ${age + 2}';

	print(greeting);// Hello everyone, my name is 승훈, I'm 32
}
```

## collection If
```dart
void main() {
	var giveMeFive = true;
	var numbers = [
		1, 
		2,
		3,
		4,
		if (giveMeFive) 5,
	];
}
```
## collection For
```dart
void main() {
	var oldFriends = ['nico', 'lynn'];
	var newFriends = [
		'lewis',
		'ralph',
		'darren',
		for(var friend in oldFriends) "❤️ $friend",
	];
	print(newFriends); // [lewis, ralph, darren, ❤️ nico, ❤️ lynn]
}
```
## QQ Operator: ??
[[노마드 코더_Dart 시작하기 3.4 QQ Operator|원본]]
- <font color="#245bdb">좌항 ?? 우항</font>
- 좌항이 null이면 우항 return
- null이 아니면 좌항 return
```dart
//사용자가 null값도 입력 가능하게 해보자
String capitalizeName(String? name) => name?.toUpperCase() ?? 'default Name';

void main() {
	capitalizaName('ead');
	capitalizaName(null);

}
```

## QQ equals(QQ assignment operator): ??=
[[노마드 코더_Dart 시작하기 3.4 QQ Operator|원본]]
- <font color="#245bdb">(변수명) ??= (값)</font>
- 값이 null이면 할당
```dart
void main() {
	String? name;
	name ??= 'ead';
	name = null;
	name ??= 'another';
}
```
## typedef
[[노마드 코더_Dart 시작하기 3.5 Typedef|원본]]
- <font color="#245bdb">typedef (타입명) = (원하는 데이터 타입)</span>
- 데이터 타입의 alias를 만듬
```dart
typedef ListOfInts = List<int>

ListOfInts reverseListOfNumbers(ListOfInts list) {
	var reversed = list.reversed;
	return reversed.toList();
}

void main() {
	print(reverseListOfNumbers([1, 2, 3])); // [3, 2, 1]
}
```
## Cascade Notation
[[노마드 코더_Dart 시작하기 4.5 Cascade Notation|원본]]
앞에 class가 있다면 그 class를 가리킴
```dart
class Player {
	String name;
	int xp;
	String team;

	Player({
		required this.name,
		required this.xp,
		required this.team,
	});

	void sayHello() {
		print("Hi my name is $name");
	}
}

void main() {
	var ead = Player(name: 'ead', xp: 1200, team: 'red');
	ead.name = 'test';
	ead.xp = 1234;
	ead.team = 'blue';

	var vic = Player(name: 'vic', xp: 1200, team: 'red')
	..name = 'test'
	..xp = 1234
	..team = 'blue';
}
```
## Enum
[[노마드 코더_Dart 시작하기 4.6 Enums|원본]]
텍스트 형태로 쓸 필요 없음
```dart
enum Team { red, blue }

class Player {
	String name;
	int xp;
	Team team;

	Player({
		required this.name,
		required this.xp,
		required this.team,
	});

	void sayHello() {
		print("Hi my name is $name");
	}
}
	var vic = Player(name: 'vic', xp: 1200, team: Team.red)
	..name = 'test'
	..xp = 1234
	..team = Team.blue;
}
```
# Dart의 함수
```dart
String sayHello(String name) {
	return "Hello $name nice to meet you!";
}

void main() {
	print(sayHello('ead'));
}
```

## fat arrow syntax
```dart
String sayHello(String name) => "Hello $name nice to meet you!";

num plus(num a, num b) => a + b;

void main() {
	print(sayHello('ead'));
}
```

## Parameter
### positional parameter
- 기본적인 parameter
- parameter의 순서가 중요
- 함수를 호출할 때 각 parameter의 위치까지 기억해야 함
- 잘 기억해서 parameter값을 입력했다하더라도 나중에 코드를 보면 한눈에 이해하기 어려움
### Named Parameters
1. 함수의 Parameter들을 중괄호로 감싸주기
2. null-safety로 인한 컴파일 에러 해결
	1. 기본값(default value)을 할당
	2. null-safety를 적용
	3. required를 사용
		- 실제 함수를 쓸 때 parameter값을 요구함
3. 함수를 호출할 때 순서에 관계없이 parameter의 이름들에 따른 값 적기
- flutter에서 자주 사용됨
```dart
String sayHello({
	required String name,
	int age = 99,
	String country = 'default Country',
}) {
	return "Hello $name, you are $age, and you come from $country";
}

void main() {
	print(sayHello(
		age: 12,
		country: 'korea',
		name: 'ead',
	));
}
```
### print()
- 뭔가를 출력하기 위한 함수