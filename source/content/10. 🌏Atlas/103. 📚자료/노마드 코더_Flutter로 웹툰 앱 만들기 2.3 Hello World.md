---
date: 2024-07-29
---
# 주제: [[Flutter]]
- `runApp()`
	- `import 'package:flutter/material.dart';`로 인해 사용 가능
	- void
	- Widget이란 타입의 하나의 argument 필요
- Widget
	- 일종의 레고블럭
	- flutter에 있는 모든건 Widget(레고블럭을 조립)
	- Class를 만들고 flutter SDK에 있는 3개의 core Widget 중 하나를 extend(상속)받아야 함
	- StatelessWidget
		- 모든 Widget은 build()를 implement(구현)해야 함
			- return하는 것을 화면에 보여줌
			- BuildContext 타입의 context 파라미터를 받음
	- root App은 MaterialApp(구글), CupertinoApp(애플) 둘 중 하나의 App을 return해야 함(우리 앱이 어떻게 보이고 싶은지 결정)
		- 구글이 만든 언어이므로 MaterialApp이 좀 더 보기 좋음
모바일 앱의 모든 화면은 scaffold(골격)가 필요