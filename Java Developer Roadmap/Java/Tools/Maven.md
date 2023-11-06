#### 검색 전 내가 아는 것
빌드하는 툴

#### 검색 후
##### Ant vs Maven
1. Ant는 비교적 자유도가 높은 편
2. Maven은 정해진 라이프사이클에 의하여 작업 수행 하며, 전반적인 프로젝트 관리 기능까지 포함.

##### Maven의 설정파일
1. setting.xml
	- 메이븐 빌드 툴과 관련한 설정 파일
	- MAVEN_HOME/conf 디렉토리에 위치
	- Maven을 build할 때, 의존 관계에 있는 라이브러리, 플러그인을 중앙 저장소에서 개발자 PC로 다운로드 하는 위치(로컬저장소)는 기본 설정 장소인 'USER_HOME/.m2/repository '이지만 setting.xml에 원하는 로컬 저장소으ㅟ 경로를 지정, 변경할 수 있다.
2. POM(Project Object Model)
	- pom.xml
	- Maven을 이용하는 Project의 root에 존재하는 xml파일
	- 모든 설정과 의존성을 확인할 수 있다.