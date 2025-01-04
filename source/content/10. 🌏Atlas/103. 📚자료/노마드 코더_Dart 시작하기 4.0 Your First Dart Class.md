---
date: 2024-07-19
---
# 주제: [[Dart]]
Dart Class
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
