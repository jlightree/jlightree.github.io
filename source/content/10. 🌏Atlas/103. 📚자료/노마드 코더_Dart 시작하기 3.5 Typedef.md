---
date: 2024-07-18
---
# 주제: [[Dart]]
typedef
typedef (타입명) = (원하는 데이터 타입)
데이터 타입의 alias를 만듬
```dart
typedef ListOfInts = List<int>

ListOfInts reverseListOfNumbers(ListOfInts list) {
	var reversed = list.reversed;
	return reversed.toList();
}

void main() {
	print(reverseListOfNumbers([1, 2, 3])); // [3, 2, 1]
}
```