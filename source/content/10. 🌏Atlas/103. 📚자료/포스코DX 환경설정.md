[POSPIA Dev Portal](dirms.posco.co.kr:7090/devportal.html)
## MSA 개발절차
### 개발환경 설치
1. jdk1.8 설치
	1. Java 8 설치
	2. 환경변수 설정
		- 사용자 변수(시스템 변수): 
			- JAVA_HOME
				- `C:\Program Files\Java\jdk1.8.0_202`
			- PATH
				- `%JAVA_HOME%\bin`
	3. 설치 확인 (cmd 창)
		- `javac -version`
2. IntelliJ 설치
	- VDI 윈도우7 기준 2023.1.5 버전 이하
	- IntelliJ 셋팅 
		1. File - Project Structure - Project - SDK 설정 확인
			- File - Project Structure - Project Settings/Project/SDK: 1.8
			- ![[20240605_080847.jpg]]
		2. File - Settings -Build, Execution, Deployment - Build Tools - Maven / Maven home path
			- `C:/Program Files/apache-maven-3.6.0`
			- ![[20240605_080856.jpg]]
3. maven 설치
	1. maven 다운로드
	2. 설치(원하는 곳에 압축 해제)
	3. 환경변수 설정
		- 사용자 변수(시스템 변수): 
			- MAVEN_HOME
				- `C:\Program Files\apache-maven-3.6.0`
	4. 설치 확인 (cmd 창)
		- `mvn -v`
	5. Maven 명령어 실행
		1. Maven 열기
		2. 재생 버튼
		3. 코드 입력
			- mvn clean package install
			- ![[20240605_080904.jpg]]
4. STS 설치
	1. 해당하는 버전을 찾아 다운로드
	2. 설치(원하는 곳에 압축 해제)
5. lombok 설치
	- lombok이 STS와 연동되어야 자동빌드시 오류가 나타나지 않습니다. 별도 설치 과정을 거치는 것을 추천합니다.
	- [lombok download](https://projectlombok.org/download)
	- lombok을 설치하기 전에 STS가 기동 상태이면 Exit 해주세요.
	- lombok.jar 실행
		- 실행방법 1: cmd 창에서 `java -jar ****.jar`
		- 실행방법 2: 파일탐색기에서 lombok.jar 우클릭 / 연결 프로그램 / java 선택
	- lombok이 STS를 잘 찾아오면 아래와 같은 IDEs에 설치된 STS가 나타납니다.
	- ![[20240531_150942.jpg]]
	- STS를 스스로 찾아오지 못하면 좌측 Specify Location버튼을 클릭해서 지정해주시면 됩니다.
	- Install/Update 버튼 선택
	- 아래와 같은 창이 뜨면 성공입니다
	- ![[20240531_150950.jpg]]
6. MES3.0 환경 설정	
	- nexus server 접근 설정
		- POSCO 내부망에서는 Maven Repository 및 기타 Repository로의 https 통신이 잘 안 됩니다.
		- 작성된 Component jar(공용 Libs)의 공유를 위해 Nexus를 활용한 Private Repository를 구축하여 사용하고 있습니다.
		- maven이 Nexus Server를 기본 Repository로 사용하도록 설정합니다.
			- [settings.xml](http://git.posco.co.kr/projects/MES3/repos/dev-file/raw/maven_env/settings.xml?at=refs%2Fheads%2Fmaster)
			- [settings-secutiry.xml](http://git.posco.co.kr/projects/MES3/repos/dev-file/raw/maven_env/settings-security.xml?at=refs%2Fheads%2Fmaster)
			- ![[20240531_154105.jpg]]
			- 위의 두개 파일을 사용자/.m2 폴더에 복사합니다.(파일명은 반드시 settings.xml과 settings-security.xml로 변경합니다.)
			- IDE maven이 사용합니다. maven설치폴더/config에 복사합니다.
			- cmd 창에서 mvn 명령 실행시 사용합니다.
7. oracle client 12 설치
	1. 기존 오라클 삭제(11g)
		- 설치된 오라클이 없으면 2번으로 넘어감
		- Oracle 11.2.0.1 Client 모듈을 깨끗이 지우려면 아래 파일을 실행하면 되는데 지우기 전에 반드시 ** TNSNAMES.ORA**파일을 백업 받으시기 바랍니다.
		1. TNSNAMES.ORA 위치 %Oracle_Home%/network/admin
		2. Oracle 삭제 실행 파일 위치 %Oracle_Home%/deinstall/deinstall.bat
	2. Oracle 12c Client 32bit 설치
		- 오렌지 사용을 위해서는 반드시 Oracle 12c Client 32Bit 버전으로 설치해야 합니다.
		- `win32_12201_client.zip`파일을 찾아서 다운 및 압축해제 합니다.
		- 설치는 런타임으로 해주시면 되겠습니다.
		1. 설치 중 오류 메세지 발생시
			- `[INS-30131]설치 프로그램 검증 실행에 필요한 초기설정을 실패했습니다.`
			- Oracle 12c Client 설치모듈 실행하여 진행 중 오류가 발생할 때
				- 커맨드창을 열고 설치파일을 압축해제한 디렉토리(`컴퓨터/D/temp/win32_12201_client/client32`)에 가서 아래 명령을 수행하여 설치해보세요.
				- 설치작업전에 환경점검을 하면서 오류가 나는데 그 과정을 건너뛰는 명령
				- `setup.exe -ignorePrereq -J"-Doracle.install.client.validate.clientSupportedOSCheck=false`
		2. 설치 진행
		3. TNS_ADMIN 환경변수 추가
			- 예시) `C:\app\client\pd299735\product\12.2.0\client_1\network\admin`tnsnames.ora가 있는 경로를 환경변수로 추가해줍니다.
			- 변수 이름: TNS_ADMIN
			- 변수 값: `C:\app\client\pd299735\product\12.2.0\client_1\network\admin`
8. orange 설치
	1. orange 다운로드
	2. DB TNS 정보 추가(Net Config Tool 클릭 후 작성 혹은 tnsnames.ora 수정)
```
NPNMTS = 
	(DESCRIPTION = 
		(ADDRESS_LIST = 
			(ADDRESS = (PROTOCOL = TCP)(HOST = 172.18.80.195)
			(PORT = 2105))
		)
		(CONNECT_DATA = 
			(SID = NPNMTS)
		)
	)
```
8. Git 설치
9. pcf CommandLineTool 설치
	- https://login.sys.dpmes.posco.co.kr/login 접속하여 각 체인 id로 로그인합니다.
	- 좌측하단 Tools 클릭
	- 해당하는 운영체제 버전 다운로드 및 설치



### 사전준비
1. Maven archetype 설치
	1. Git에서 mavenArchetype download (최신 버전 0.0.6)
	2. local repository에 install
	3. maven project -> base 프로젝트 형식 선택
		1. mvn명령어를 통해 프로젝트 구조 생성
			1. Git Bash 실행 후 명령 창에서 아래 명령어 샐행
				- `mvn archetype:generate -DarchetypeGroupId=com.posco.reuse -DarchetypeArtifactId=microservice-archetype -DarchetypeVersion=1.0.0-SNAPSHOT -DgroupId=[com.it] -DartifactId=[sample] -DbizDomain=ProductHistory -DbizApp=Product`
				- groupID와 artifactID는 Chain에 맞게 수정
				- m2h chain 지시서비스의 경우
					- com.posco.mes3.m2h
					- m2hb01-order
			2. 버전 및 생성자 정보 입력
				- ![[20240605_112758.jpg]]
				- Figure 10mvn 명령어 실행 화면
		2. 생성된 프로젝트 구조 빌드 및 실행
			1. 프로젝트 빌드
				- 생성된 프로젝트 폴더로 이동하여 mvn clean install 실행
				- `BUILD SUCCESS`메세지가 표시되어야 함
			2. 프로젝트 실행
				- boot 프로젝트의 target 디렉토리에서 java -jar 프로젝트명 -boot-1.0.0-SNAPSHOT.jar 실행
				- `java -jar test-boot-1.0.0-SNAPSHOT.jar`
				- ![[20240605_113121.jpg]]
		3. API 테스트
			1. swagger-ui.html을 통한 API 수행
				- 브라우저에서 http://localhost:8080/swagger-ui.html 호출 후 각 API 정상 동작 여부 확인
				- ![[20240605_113312.jpg]]
	4. Read-Only Microservice의 경우
		- Read-Only Microservice 생성 및 실행 방법은 일반 Microservice와 동일하다. 다만, mvn 명령 실행 시 archetype만 microservice에서 readonly로 변경하면 된다.
		- `mvn archetype:generate -DarchetypeGroupId=com.posco.reuse -DarchetypeArtifactId=readonly-archetype -DarchetypeVersion=1.0.0-SNAPSHOT -DgroupId=[com.it] -DartifactId=[sample] -DbizDomain=ProductHistory -DbizApp=Product`
		- [ReadOnly ArcheType ReadMe](https://git.posco.co.kr/projects/POSCO-ARCHETYPE/repos/readonly-archetype/browse/readme.md)
	5. batch Microservice의 경우
		- Batch Microservice 생성 방식은 일반 Microservice와 동일하다.다만, mvn 명령 실행 시 archetype만 microservice에서 batch로 변경하면 된다.
		- `mvn archetype:generate -DarchetypeGroupId=com.posco.reuse -DarchetypeArtifactId=batch-archetype -DarchetypeVersion=1.0.0 -DgroupId=[com.it] -DartifactId=[sample] -DbizDomain=ProductHistory -DbizApp=Product`
		- [Batch ArcheType ReadMe](https://git.posco.co.kr/projects/POSCO-ARCHETYPE/repos/batch-archetype/browse/readme.md)
		- 다른 Microservice와 달리 Batch Microservice는 build전에 db-local.properties파일에 DB연결 정보를 작성해야 한다.
		- ![[20240605_142940.jpg]]
		- 또한, mvn install 수행 후 실행 방법도 아래와 같이 DB 정보를 관리하는 properties 파일 경로를 지정하고, 실제 실행될 Job 명을 파라미터로 넘겨주어야 한다.
		- 다른 Microservice들은 서비스가계속 실행되는 상태이나, 배치의 경우 한번 수행되고 종료되게된다.
		- `java -jar -Ddb="C:\archeTest\sample4\src\main\resources\db-local.properties" sample4-batch-1.0.0-SNAPSHOT.jar ProductHistoryRunner`
2. bootstrap.yml
	1. 초기 기동시 Config Server에 자신의 Service명과 Active Profile명을 제시하고 설정 정보를 받아오기 위한 Config server 관련 정보 작성
	2. 이 설정 정보를 바탕으로 DB Connection등의 초기화를 진행하며 구동 (참고: "Config First Bootstrap" mode 기준)
		- ![[20240605_143905.jpg]]
3. application.yml
	1. git의 config-repo에 새로운 디렉토리 생성(어플리케이션 이름과 동일)
	2. aplication-${profile}.yml 추가
```
application.yml

spring:
  datasource: # database 관련 설정
    url: ${datasource.uri}
    username: ${datasource.username}
    password: ${datasource.password}
    driver-class-name: ${datasource.driver.class.name}
    hikari:
      maximum-pool-size: 2 # DB connection pool 조정 위함 (Default : 10) 2~3으로 축소 조정 필요
      data-source-properties:
        implicitCachingEnabled: true
        oracle.jdbc.implicitStatementCacheSize: 50 # jdbc cache 설정
  jpa:
    hibernate:
      ddl-auto: ${jpa.hibernate.ddl-auto}
    database: ${jpa.database}
    show-sql: true
    properties:
      hibernate:
        format_sql: true
  jackson: # json에서 null이 아닌 값만 전달 받기 위한 설정
    default-property-inclusion: NON_NULL

  cloud:
    stream:
      kafka:
        binder:
          zk-nodes:
          - 172.18.80.172:2181
          brokers:
          - 172.18.80.172:9092
      bindings:
        input:
          destination: inputTopic
        output:
          destination: outputTopic
  kafka:
    producer:
      bootstrap-servers:
      - 172.18.80.172:9092

###
#   swagger Settings
###
swagger:
  basePackage: 'com.posco.mes3'
  title: 'service-name Service'
  description: 'service-name Service api document & api tester'
  termsOfServiceUrl: 'http://${callgate.uri}:${callgate.port}/service-name'
```
```
application-local.yml #local 환경에서 service설정 작성

server:
	port: 8088

eureka:
	server:
		ip: bureau-service
		port: 8082

callgate:
	uri: callgate-service
	port: 8080

datasource:
	driver.class.name: org.h2.Driver
	uri: jdbc:h2:file:~/test
	username: sa
	password:

jpa:
	hibernate:
		ddl-auto: none
	database: h2
```



