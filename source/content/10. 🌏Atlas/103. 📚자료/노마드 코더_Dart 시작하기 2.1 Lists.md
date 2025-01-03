---
date: 2024-07-17
---
# 주제: [[Dart]]
Flutter에서 유용
`var numbers = [1, 2, 3, 4, 5];`
`List<int> numbers = [1, 2, 3, 4, 5];`
몇몇 IDE에서는 List의 끝 요소 뒤에 ','를 붙여주면 자동으로 여러 줄로 포매팅
collection if, collection for 지원

collection if
```dart
void main() {
	var giveMeFive = true;
	var numbers = [
		1, 
		2,
		3,
		4,
		if (giveMeFive) 5,
	];
}
```
