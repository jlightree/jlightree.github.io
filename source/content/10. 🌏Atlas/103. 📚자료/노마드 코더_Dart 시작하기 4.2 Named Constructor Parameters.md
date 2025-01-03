---
date: 2024-07-19
---
# 주제: [[Dart]]
Named Constructor Parameters
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