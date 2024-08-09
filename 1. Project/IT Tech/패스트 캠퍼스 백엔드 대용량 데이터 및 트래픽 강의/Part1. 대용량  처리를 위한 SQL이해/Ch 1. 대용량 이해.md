# 목차
1. [01. 강의 소개](#ch-01-강의-소개)
2. [02. Orientation](#ch-02-orientation)
3. [03. 실습환경 구축](#ch-03-실습환경-구축)
# 01. 강의 소개
# 02. Orientation
# 03. 실습환경 구축
## MariaDB(MySQL) 설치

강의에선 MySQL을 그냥 설치했지만 좋은 개발 환경을 위해서 Docker를 설치하고 Docker위에서 DB시스템을 구축하는 방향로 잡았다. 
### 맥
#### 개요
Mac에서 개발환경을 구축하려면 HomeBrew의 설치는 필수이기 때문에 강의 내용을 따라 HomeBrew를 설치하는 과정을 넣었다. Docker를 설치하면 HomeBrew를 활용하여 DB를 로컬에 설치하지 않기 때문에 사실 DB 환경 세팅에서는 HomeBrew를 사용하지 않는다. 강의에서는 MySQL을 설치하여 Intellij와 연결했지만 MySQL 개발자들이 MySQL을 나와 MariaDB를 제작했기때문에 MySQL대신 MariaDB로 DB환경을 Docker Container에서 구축한다.
#### 1. HomeBrew 설치
[Homebrew](https://brew.sh/)
Mac 터미널에서 아래 Command를 입력하면 HomeBrew가 설치된다.
```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

#### 2. Docker 설치
[Docker Desktop](https://docs.docker.com/desktop/install/mac-install/)에서 맥의 프로세서에 맞는 설치파일을 받아 순서에 맞게 설치를 진행하면 된다. 설치 파일 링크 아래에 설치 과정에 대해서 자세한 설명이 있으니 참고하면 된다.

#### 3. MariaDB Container 설치
##### 1. Docker Image 가져오기
터미널을 열고 아래 Command를 입력해서 Docker Hub에서 MariaDB Image를 다운로드 한다.
```bash
docker pull mariadb
```
아래 Command를 통해 다룬로드된 Image를 확인한다.
```bash
docker image
```
위의 방법으로 제대로 진행이 되지 않는다면 docker desktop을 실행해서 mariadb image를 찾아서 pull 하면 된다.

##### 2. MariaDB 컨테이너 생성 및 실행
아래의 Command를 통해 MariaDB 컨테이너를 생성할 수 있다.
```bash
docker run -p 3306:3306 --name {컨테이너 이름 작성} -e MARIADB_ROOT_PASSWORD={비밀번호} -d mariadb
```
> ex) docker run -p 3306:3306 --name mariadb -e MARIADB_ROOT_PASSWORD=1111 -d mariadb

위 Command의 의미는 다음과 같다.
- **-p** 3306:3306 : 호스트와 컨테이너 간의 포트를 연결 (host-port:container-port),  호스트에서 3306 포트 연결 시 컨터이너 3306 포트로 포워딩
- **--name** {컨테이너 이름} : 생성하려는 컨테이너의 이름을 {컨테이너 이름} 으로 생성한다.
- **-e** MARIADB_ROOT_PASSWORD={비밀번호} : 컨테이너의 환경 변수 설정. MARIADB_ROOT_PASSWORD는 root사용자의 암호를 설정한다는 뜻이며 root사용자의 비밀번호를 {비밀번호} 정한다는 뜻이다.
- **-d** 컨테이너를 백그라운드에서 실행한다는 뜻이다.
아래 Command를 통해 컨테이너를 조회할 수 있다.
```bash
// 실행 중인 컨테이너만 조회
docker ps

// 모든 컨테이너 조회
docker ps -a
```
##### 3. MariaDB에 접속하기
컨테이너를 성공적으로 생성하고 실행이 되면 아래 Command를 통해 MariaDB에 접속할 수 있다.
```bash
docker exec -it {컨테이너 이름} mariadb -uroot -p
```

##### 4. DataBase 생성
MariaDB에 접속 성공했으면 DataBase를 생성한다.
```sql
CREATE DATABASE {database_name};
```
MariDB콘솔에서 CREATE DATABASE {데이터베이스 이름}를 통해 DataBase를 생성할 수 있다.
강의에서 fast_sns로 DataBase를 생성했기 때문에 아래 SQL문으로 fast_sns DataBase를 생성한다.
```sql
CREATE DATABASE fase_sns;
```
![[Pasted image 20231021223517.png]]
DataBase가 정상적으로 생성이 됐는지 확인하기 위해 아래 Query문을 통해 확인한다.
```sql
SHOW DATABASES;
```
![[Pasted image 20231021223420.png]]
정상적으로 DataBase가 생성됐으면 아래 Query문을 통해 MariaDB 콘솔을 종료하고 나온다.
```sql
exit;
```


-----
###### Reference
[Homebrew](https://brew.sh/)
[Install Docker Desktop on Mac](https://docs.docker.com/desktop/install/mac-install/)
[Docker 컨테이너에 MariaDB 설치하기](https://dkswnkk.tistory.com/697)
[MariaDB Official Site](https://mariadb.com/)
[MariaDB Download](https://mariadb.com/downloads/)
[MariaDB Documant - CREATE DATABASE](https://mariadb.com/kb/en/create-database/)







## IDE와  DB연결
### Intellij
#### 1. Intellij 오른쪽 리본 메뉴에서 DataBase 메뉴 클릭
#### 2. DataBase 메뉴의 상단 버튼 중 + 클릭
#### 3. Data Sources and Drivers 메뉴를 눌러 창 열기
#### 4. DataSource 탭에서 + 버튼을 눌러 연결할 DB 시스템을 선택
#### 5. 선택한 DB 시스템 상세 창에서 User와 Password, DataBase를 입력
##### 1. Driver 설치 알림
###### 1. 상세 창에서 해당 DB의 Driver가 설치되어 있지 않으면 해당 Driver의 설치 알림
###### 2. 상세 창 General 탭의 상단에서 Driver를 클릭하여 Driver 탭으로 이동하여 해당 Driver 설치 진행

#### 6. TestConnect를 클릭하고 접속에 성공하면 Ok버튼을 눌러 창을 닫는다.
#### 7. Project 상에서 DB연결
1. 1.src/main/resources/application.properties 열기
2. ${url} 지우고 mysql endpoint와 데이터베이스 입력
	ex) localhost:3306/fast_sns 
3. password의 mysql 비밀번호 입력
#### 8. Build Config를 FastcampusMysqlApplication로 맞춰놓고 Run을 눌러 빌드하고 프로젝트를 실행한다.
##### <span style="color:red">Error 발생시</span>
- Gradle Build 방식 : [MariaDB Connect Gradle Info](https://mariadb.com/kb/en/java-connector-using-gradle/)
- Maven Build 방식 :
#### 9. 성공적으로 빌드가 성공 적으로 완료가 됐다면 [local page](http://localhost:8080/swagger-ui.html)로 접속해서 API를 확인해본다.
##### 1. local page에 접속하게 되면 hello-world-controller API를 확인할 수 있다.
##### 2. hello-world-controller API는 GET방식으로 Try it out 버튼을 누르고 execute를 실행해서 200 코드를 응답 받으면 정상적으로 프로젝트가 동작한다는 뜻이다.

##### <Span Style="color:red">Error List</Span>
##### Execution failed for task ':compileJava'.
(https://mincanit.tistory.com/11)

##### Data base 외부 접속 불가 현상
error
DBMS: MariaDB (no ver.)
Case sensitivity: plain=mixed, delimited=exact
[HY000][1130] Host 'host.docker.internal' is not allowed to connect to this MariaDB server.

solution
[MySQL 외부 접속 불가능 현상 해결 방법(접근 권환)](https://veneas.tistory.com/entry/MySQL-MySQL-%EC%99%B8%EB%B6%80-%EC%A0%91%EC%86%8D-%EB%B6%88%EA%B0%80%EB%8A%A5-%ED%98%84%EC%83%81-%ED%95%B4%EA%B2%B0-%EB%B0%A9%EB%B2%95-%EC%A0%91%EA%B7%BC-%EA%B6%8C%ED%95%9C)

