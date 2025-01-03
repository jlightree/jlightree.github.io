---
date: 2024-07-12
---
# 주제: [[Dart]]
## Dart의 특징
- UI에 최적화
- 생산적인 개발환경
- 모든 플랫폼에서 빠름
- 컴파일러
	- Dart Web
		- Dart로 쓴 코드를 javascript로 변환
	- Dart Native
		- Dart로 쓴 코드를 여러 CPU의 아키텍쳐에 맞게 변환
		- ARM32
		- ARM64(대부분의 모바일 기기)
		- x86_64(데스크탑)
		- JIT(just-in-time)
			- Dart VM 사용
				- 코드의 결과를 바로 화면에 보여줌
		- AOT(ahead-of-time)
			- 컴파일시 아키텍처를 지정
			- 해당하는 아키텍처에 대한 바이너리(machine code)로 컴파일하여 바이너리 배포
			- 단점 
				- UI를 개발시엔 느림
				- 뭔가 하나를 바꿔도 그 바꾼 것에 대한 결과를 위해 처음부터 끝까지 컴파일 해야 함
		- 개발할땐 JIT, 배포할 땐 AOT
	- => IOS, Android, Windows, Linux, Mac 등등으로 컴파일 가능
- null safety
	- 안전한 프로그램을 빌드할 때 중요
- flutter가 Dart를 선택한 이유
	1. JIT 컴파일과 AOT 컴파일이 둘 다 있음
		- ⇒ 모바일 개발에 아주좋은 언어(빠른 피드백, 빠른 최종 앱)
	2. Dart와 Flutter 둘 다 구글에서 만듬
		- ⇒ Flutter를 위해 Dart 최적화 가능