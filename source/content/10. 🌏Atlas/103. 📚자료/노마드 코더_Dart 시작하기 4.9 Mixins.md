---
date: 2024-07-23
---
# 주제: [[Dart]]
Mixins
- 생성자가 없는 클래스
- 내부의 프로퍼티와 메소드들을 가져옴
```dart
class Strong {
	final double strengthLevel = 99.99;
}
class QuickRunner {
	void runQuick() {
		print("Run!!");
	}
}

class Tall {
	final double height = 1.99;
}

enum Team { blue, red }

class Player with Strong, QuickRunner, Tall {
	final Team team;
}

class Horse with Strong, QuickRunner {}
```