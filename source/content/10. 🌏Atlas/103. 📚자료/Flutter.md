# Flutter의 특징
[[노마드 코더_Flutter로 웹툰 앱 만들기 1.3 How Flutter Works|원본]]
- Flutter 혹은 Dart 코드는 운영체제와 직접 소통 불가([[개발용어#네이티브 프레임워크|네이티브 프레임워크]]가 아님)
- ![[Pasted image 20240724132242.png]]
	- Dart로 짠 코드는 Flutter Framework 상에서 이용
	- 화면에 뿌려줄 때(렌더링) 운영체제와 직접 대화하는 것이 아닌 엔진을 사용
		- C/C++ 사용
		- 무언가를 그려주는 역할
		- Flutter 어플리케이션은 엔진이 버튼 등등의 것을 다 그려주기 때문에 플랫폼의 Native Widget을 사용하지 않음
- 운영체제는 엔진을 동작, 엔진은 Dart 코드 동작, 화면에 UI 그림
- 유저가 앱을 다운받아 실행하면 엔진이 runner를 열음, runner 프로젝트는 엔진 실행, 엔진이 UI 렌더링
- 네이티브 앱들이 가지는 컴포넌트나 위젯들을 가질 수 없음([[노마드 코더_Flutter로 웹툰 앱 만들기 1.4 Flutter vs React Native|원본]])
	- ⇒ iOS 스타일의 앱을 만들고싶다면 네이티브 앱으로 만들어야 함
- 완전한 객체지향 프레임워크(=모든게 다 class))

# runApp()
[[노마드 코더_Flutter로 웹툰 앱 만들기 2.3 Hello World|원본]]
```dart
import package:flutter/material.dart;

void main() {
	// Widget 타입의 App 클래스를 argument로
	void runApp(App());
}
```
## rootApp()
```dart
import 'package:flutter/material.dart';

void main() => runApp(App());
// flutter SKD에 있는 3개의 core Widget 중 하나인 StatelessWidget 상속(extend)
class App extends StatelessWidget {
	// 모든 Widget은 build()를 구현(implement)해야 함
	@override
	Widget build(BuildContext context) {
		// 구글이 만든 MaterialApp을 return
		return MaterialApp(
			// scaffold(골격)
			home: Scaffold(
				appBar: AppBar(
					title: Text("Hello flutter!"),
				),
				body: Center(
					child: Text("Hello World!"),
				),
			),
		);
	}
}
```
- MaterialApp(구글), CupertinoApp(애플) 둘 중 하나의 App을 return해야 함(우리 앱이 어떻게 보이고 싶은지 결정)
	- 구글이 만든 언어이므로 MaterialApp이 좀 더 보기 좋음
- 모바일 앱의 모든 화면은 scaffold(골격)가 필요
- [[#Widget]]에 대한 설명 참고

# 용어
### Widget
[[#rootApp()|code 참고]]
- 일종의 레고블럭
- flutter에 있는 모든건 Widget(레고블럭을 조립)
- Class를 만들고 flutter SDK에 있는 3개의 core Widget 중 하나를 extend(상속)받아야 함
- 모든 Widget은 build()를 implement(구현)해야 함
	- build()
		- return하는 것을 화면에 보여줌
		- BuildContext 타입의 context 파라미터를 받음
- 사용할 때마다 class를 인스턴스화 해야 함([[노마드 코더_Flutter로 웹툰 앱 만들기 2.5 Classes Recap|원본]])
- Reusable Widgets [[노마드 코더_Flutter로 웹툰 앱 만들기 3.5 Reusable Widgets|예시 코드]]
#### padding
여백
#### SizedBox()
Size가 있는 Box, 공간을 만들 때 사용
# VSCode Settings
[[노마드 코더_Flutter로 웹툰 앱 만들기 3.3 VSCode Settings|원본]]
- 파란 줄의 경고
	- constant constructors는 const 사용 추천한다는 의미 ^3fc12c
	- Dart는 constant(상수)개념을 지원
	    - constant value(변수)는 값을 사전(compile 전)에 알 수 있으므로 Dart compiler가 vlaue를 위한 메모리 공간을 만드는 대신 value가 있는 곳에 constant(상수)로 대체
	- 상수가 될 수 있는 것이 무엇인지 기억하고 입력해주는 것인 매우 번거롭기에 setting.json을 통해 [[#^3fc12c|경고]] 해결
		- Command Palette에서 'open user settings' 입력 ⇒ setting.json 파일이 열림
		- `"editor.codeActionsOnSave": { "source.fixAll": true },` 추가
		- 저장할 때마다 const가 자동으로 추가
- Widget별로 부모가 무엇인지 알려주는 줄 생성
	- `"dart.previewFlutterUiGuides": true,`추가
	- VSCode 다시 시작