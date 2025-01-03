---
date: 2024-07-23
---
# 주제: [[Dart]]
Abstract Class(추상화 클래스)로는 객체 생성 불가
다른 클래스들이 직접 구현해야하는 메소드들을 모아놓은 일종의 청사진
메소드의 이름과 반환 타입만 정의 가능
특정 메소드를 구현하도록 강제
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