---
date: 2024-07-18
---
# 주제: [[Dart]]
collection For와 collection If는 UI 인터페이스를 만들 때 유용
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