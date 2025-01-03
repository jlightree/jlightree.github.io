---
date: 2024-08-13
---
# 주제: [[Flutter]]
## VSCode Settings
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