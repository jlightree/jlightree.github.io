---
date: 2024-07-18
---
# 주제: [[Dart]]
QQ Operator: ??
<font color="#245bdb">좌항 ?? 우항</font>
좌항이 null이면 우항 return
null이 아니면 좌항 return
```dart
//사용자가 null값도 입력 가능하게 해보자
String capitalizeName(String? name) => name?.toUpperCase() ?? 'default Name';

void main() {
	capitalizaName('ead');
	capitalizaName(null);

}
```

QQ equals(QQ assignment operator): ??=
<font color="#245bdb">(변수명) ??= (값)</font>
값이 null이면 할당
```dart
void main() {
	String? name;
	name ??= 'ead';
	name = null;
	name ??= 'another';
}
```