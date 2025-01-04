---
date: 2024-07-18
---
# 주제: [[Dart]]
Map
JavaScript나 TypeScript의 object
phthon의 dictionary같은 것
```dart
void main() {
	var player = {
		'name': 'ead',
		'xp': 19.99,
		'superPower': false,
	}
}
```
=> Map<String, Object>: key(String)와 value(Object)로 이뤄져있음

데이터타입 직접 선언
```dart
void main() {
	Map<int, bool> player = {
		1: true,
		2: false,
	}
}
```
key와 value에 어떤 것도 명시 가능