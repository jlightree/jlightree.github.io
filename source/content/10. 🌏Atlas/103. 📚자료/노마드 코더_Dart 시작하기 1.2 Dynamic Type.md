---
date: 2024-07-15
---
# 주제: [[Dart]]
## dynamic
- 여러가지 타입을 가질 수 있는 변수에 쓰는 키워드
- 사용되는게 추천되진 않지만 때때로 유용
```dart
void main() {
	var name;
	name = '승훈';
	name = 12;
	name = true;
}
```
- 변수의 타입이 dynamic이 되어 여러 타입을 선언할 수 있음
- dynamic이 필요한 경우
	- 변수가 어떤 타입인지 알기 어려운 경우
		- 특히 flutter나 json이랑 함께 작업하면 자주 발견 가능
	- dynamic으로 돌아가는게 더 유용할 경우
```dart
void main() {
	dynamic name;
	name = '승훈';
	name = 12;
	name = true;
}
```
- dynamic이라고 직접 명시도 가능
- Dart가 dynamic을 통해 변수의 기능을 제한함
```dart
void main() {
	dynamic name;
	if(name is String) {
		name.//String에 관한 옵션 제공
	}
	name.//dynamic에 관한 몇가지의 옵션만 제공
}
```