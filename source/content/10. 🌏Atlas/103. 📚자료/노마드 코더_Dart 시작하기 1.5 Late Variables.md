---
date: 2024-07-16
---
# 주제: [[Dart]]
late
- final이나 var 앞에 붙여줌
- (필요한 데이터가 아직 없을 수 있으므로) 데이터 없이 변수를 만듬
```dart
void main() {
	late final String name;
	// do something, maybe go to API
	name = '승훈';
}
```
- 값을 넣기 전에 변수를 사용하려 하면 Dart가 사용하면 안된다고 알려줌(null safety와 유사)
```dart
void main() {
	late final String name;
	// do something, maybe go to API
	print(name); // 에러
}
```
- flutter로 data fetching 할 때 정말 유용