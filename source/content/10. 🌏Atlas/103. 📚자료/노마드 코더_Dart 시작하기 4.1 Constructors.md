---
date: 2024-07-19
---
# 주제: [[Dart]]
constructor
late를 통해 변수들의 값을 나중에 받아올 것임을 인지시킴
class 이름을 그대로 써서 constructor를 만듬
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
더 간결하게 하는 법
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