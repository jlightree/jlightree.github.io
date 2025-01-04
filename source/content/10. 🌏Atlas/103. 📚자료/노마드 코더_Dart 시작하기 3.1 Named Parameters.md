---
date: 2024-07-18
---
# 주제: [[Dart]]
flutter에서 자주 사용됨
순서에 관계없이 argument의 이름들만 확실히 적어주면 됨
함수의 Parameter들을 중괄호로 감싸주기만하면 null-safety때문에 에러가 나므로 기본값(default value)을 작성해주거나 null-safety를 적용시켜주면 됨
required를 사용하면 실제 함수를 쓸 때 parameter 값을 요구해서 안전
```dart
String sayHello({
	required String name,
	int age = 99,
	String country = 'default Country',
}) {
	return "Hello $name, you are $age, and you come from $country";
}

void main() {
	print(sayHello(
		age: 12,
		country: 'korea',
		name: 'ead',
	));
}
```