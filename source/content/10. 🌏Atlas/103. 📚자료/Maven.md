상위 파일: [[🧭공부#Back-end]]

## 프로젝트 관리를 위한 도구
- 메이븐은 프로젝트의 생성, 배포 및 리포팅까지 전체 과정을 관리하는 도구다.
- 해당 프로젝트에서 사용하는 라이브러리에 대한 종속성 관리를 편하게 할 수 있다.
- 프로젝트의 버전 관리가 가능하다.
- 프로젝트 구조의 일관성을 부여한다.
- 컴파일, 테스트, 배포까지 자동화된 빌드 프로세스를 제공한다.
![[Maven의 빌드 과정.jpg]]

## Lifecycle
- 메이븐에서 빌드되는 전체 과정을 <span style="color: blue">라이프사이클</span>이라 한다.
- 라이프사이클의 각 단계는 <span style="color: blue">페이즈(Phase)</span>라고 하며 각 페이즈는 플러그인(Plugin, **POM.xml 파일을 통해 설정한 플러그인**)을 기반으로 동작한다.
	- 플러그인을 추가, 삭제함으로 디테일한 페이즈 설정이 가능하다.
- 하나의 플러그인은 여러 작업을 수행할 수 있으며 실행 가능한 각각의 작업을 <span style="color: blue">골(Goal)</span>이라고 한다.
- 라이프사이클은 페이즈 단위로 빌드하며, 페이즈 실행 시 연결된 플러그인의 골(각각의 작업)을 실행하는 구조로 동작한다.

## Dependency Management
- 처음 메이븐 프로젝트를 구성하면 우선적으로Library 설정(<span style="color: blue">Dependency Management</span>)을 해야 한다.
	- <span style="color: blue">Dependency Management</span>(Library 설정): 프로젝트마다 사용하는 Library가 다르며, 그 프로젝트에 맞는 Library들을 프로젝트에 적용할 수 있게끔 하는 것
	- 스프링 기반의 웹 프로젝트를 만들 때, <span style="color: green">스프링 웹과 관련된 파일들(`~~.jar`)</span>
	- json파일을 변환할 때 <span style="color: green">변환해주는 라이브러리 파일들(.gson)</span>
	- getter/setter를 편하게 쓰기 위한 <span style="color: green">lombok 라이브러리</span>
	- 위와 같은 <span style="color: green">다양한 라이브러리들</span>을 개발자가 손쉽게 사용할 수 있게 해주는 것이 <span style="color: blue">Dependency Management</span>
	- ⇒ [[Maven#pom.xml|pom.xml]](메이븐 프로젝트의 설정 파일)에 필요한 라이브러리들을 명시해놓으면 메이븐이 관련 라이브러리들을 다운받아서 프로젝트에 사용할 수 있도록 해준다.
- 메이븐이 프로젝트에서 라이브러리를 어떻게 다루는지
	- <span style="color:blue">Central Repository</span>: 우리가 사용하고 싶은 라이브러리가 있는 곳
	- <span style="color: blue">Central Repository</span>에서 Network를 통해 <span style="color: blue">Local(내가 있는 곳)</span>로 라이브러리를 가져온다.
	- ![[tempFileForShare_20240514-084955.jpg]]
	- <span style="color: blue">Local Repository</span>에서 각각의 개발자들이 같은 버전의 라이브러리를 사용해야 하기에 <span style="color: blue">Internal Network</span> 상에서 <span style="color: blue">Remote Repository</span>를 설정한다.
	- <span style="color: blue">Remote Repository</span>에 프로젝트에서 사용하는 라이브러리들을 <span style="color: blue">Central Repository</span>에서 가져오고 가져온 라이브러리들을 <span style="color: blue">Local Repository</span>에서 관리해서 사용한다.
- 의존 라이브러리 관리 기능은 라이프사이클과 마찬가지로 메이븐의 중심이 되는 기능 중 하나다.
- 라이브러리관리를 위한 저장소는 <span style="color: blue">중앙(Central) 저장소</span>, <span style="color: blue">원격(Remote) 저장소</span>, <span style="color: blue">로컬(Local) 저장소</span>로 구분된다.
- <span style="color: blue">중앙 저장소</span>는 오픈 소스 라이브러리, 플러그인, 아키타입을 관리하는 저장소다.
- <span style="color: blue">원격 저장소</span>는 내부망에 구축하는 저장소, 혹은 중앙 저장소에 없는 별개의 라이브러리저장소를 뜻한다.
- <span style="color: blue">로컬 저장소</span>는 개발자 컴퓨터의 저장소로 USER_HOME/.m2/repository의 위치를 갖는다.
	- 라이브러리에 이상이 있을 때 .m2폴더의 repository폴더를 비우고 다시 라이브러리들을 받아주면 해결가능할 수 있다.

## Maven 프로젝트
- archetype: 템플릿
- Artifact Coordinates
	- GroupId, ArtifactId: 프로젝트를 유니크하게 구분하기 위한 이름의 대분류, 소분류의 개념
	- GroupId: 일반적으로 url을 뒤집어서 만든다.
	- ArtifactId: 프로젝트의 이름정도

## pom.xml
- 플러그인 설정
- 라이브러리 설정
	- 특정 라이브러리를 사용하기 위해 `<dependencies></dependencies>`태그 안에 사용하고자하는 라이브러리의 groupId, artifactId, version 등을 명시하면 해당하는 라이브러리들을 Local Repository까지 가져온다.
	- Central Repository에 갖고오고 싶은 라이브러리들이 어떤 형태로 있는지 알아야 한다. [Maven Central Repository](https://mvnrepository.com)
	- Maven Central Repository에서 Maven에 해당하는 dependency를 알 수 있다.
- 프로퍼티 설정