---
date: 2024-07-23
---
# 주제: [[Dart]]
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