---
date: 2024-07-19
---
# 주제: [[Dart]]
Named Constructors
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