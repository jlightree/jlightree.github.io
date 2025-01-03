---
date: 2024-07-23
---
# 주제: [[Dart]]
super 키워드를 통해 (확장을 한) 부모 클래스와 상호작용(프로퍼티 접근, 메소드 호출)
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