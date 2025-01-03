---
date: 2024-07-17
---
# 주제: [[Dart]]
String Interpolation
text에 변수를 추가하는 방법(flutter에서 사용)
(작은 따옴표나 큰 따옴표 내에서)<font color="blue">'$(변수명)'</font>
계산이 필요할 때
<font color="blue">'${(변수명) + 계산}'</font>
```dart
void main() {
	var name = '승훈';
	var greeting = 'Hello everyone, my name is $name, nice to meet you!';

	print(greeting);// Hello everyone, my name is 승훈, nice to meet you!
}
```