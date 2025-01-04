---
date: 2024-07-16
---
# 주제: [[Dart]]
## null safety
기본적으로 모든 변수는 non-nullable(null이 될 수 없음)
개발자가 null 값을 참조할 수 없게 함
null 참조시엔 런타임 에러(사용자가 앱을 사용하는 중에 뜨는 에러)가 뜸
null을 참조하기 위해선 어떤 변수, 데이터가 null이 될 수 있음을 명시해줘야 함
### null safety를 사용하지 않은 경우
```dart
// Without null safety:
bool isEmpty(String string) => string.length == 0;

main() {
	isEmpty(null);
}
```
NoSuchMethodError가 뜸
그렇다고 null을 없앨수는 없음
null(부재, 아무것도 있지 않음)은 언어에서 유용함

### null safety 사용
Dart에서는 어떤 변수가 null이 될 수 있음을 정확히 표시해야 함
```dart
void main() {
	String? name = '승훈';
	name = null;
	if (name != null) {
		nico.isNotEmpty;
	}
	// 단축 문법
	name?.isNotEmpty;
}
```