---
date: 2024-07-19
---
# 주제: [[Dart]]
Flutter에서 class가 전부이므로 constructor를 잘 이해하는 것이 중요
기본 Constructor와 Named Constructor의 차이를 이해하고 문법의 작동방식을 이해해야 함

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