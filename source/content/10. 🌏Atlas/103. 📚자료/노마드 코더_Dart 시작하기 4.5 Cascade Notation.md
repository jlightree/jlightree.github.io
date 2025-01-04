---
date: 2024-07-23
---
# 주제: [[Dart]]
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