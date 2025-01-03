---
date: 2024-07-18
---
# 주제: [[Dart]]
```dart
String sayHello(String name) {
	return "Hello $name nice to meet you!";
}

void main() {
	print(sayHello('ead'));
}
```
void: return nothing

fat arrow syntax
```dart
String sayHello(String name) => "Hello $name nice to meet you!";

num plus(num a, num b) => a + b;

void main() {
	print(sayHello('ead'));
}
```