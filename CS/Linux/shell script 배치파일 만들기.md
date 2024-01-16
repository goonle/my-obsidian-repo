---

---

### 왜 Shell Script를 만들려고 하는가?
---
회사에서 개발 중인 프로젝트가 있다. 대략적인 설계는 끝났지만 방향성이 바뀌는 경우가 잦아 DataBase가 자주 변하고 있다. 여러 명의 개발자가 서로 다른 메뉴를 개발 중이기 때문에 DataBase의 일관성을 유지하고자 하나의 DataBase를 모두가 바라보는 상태다. 

그 상태에서 해당 DB가 날리는 실수를 하게 되었다. 

다행히도 백업해둔 파일이 있어 금방 복구했지만 완제품이 나오기 전까지 계속해서 변화하는 DB를 하루 단위로 백업을 시켜야 할 필요성을 느꼈고 그 작업을 전담하는 사람이 생겼다.

> **"간단한 작업인데 자동으로 하면 안될까?"** 

위의 생각으로 내가 아는 지식 내에서 생각해보니 아래와 같이 정리되었다.
```bash
1. shell script로 db 백업을 해봤다.
2. 분명히 스케줄링으로 리눅스에서 특정시간에 스크립트를 실행할 수 있을 것이다.
```
이 해결방안이 Shell script 파일이었다.

### 알아야 할 지식
---
#### Shell 이란?
> [!info]
> 사용자로부터 받은 명령을 kernel이 이해하도록 해석하여 전달하는 명령어 해석기

- 리눅스의 경우
	- /bin/sh : 표준 쉘로 복구 모드에 사용된다.
	- /bin/bash : 리눅스에서 대표적으로 사용하는 쉘

#### Shell script
>[!info]
>스크립트(파일)에 명령어를 전부 적고 한번에 실행되도록 만들 수 있는데 이렇게 만든 파일들을 shell script, batch file이라고 부른다.


### Shell script 만드는 방법 (Linux)
---
만드는 방법은 간단하다.
1. shell_script_file_name.sh 처럼 확장자명이 sh인 파일을 만든다.
2. 내용을 적는다.
3. 실행한다.

#### 1. sh 파일을 만든다.
```bash
cd /opt
touch shell_script_file_name.sh
```
#### 2. 내용을 적는다
리눅스의 경우 상단에 명령어를 해설할 때 사용할 쉘을 표기해야 한다.
나의 경우, postgreSQL을 사용했고, 특정 prefix를 가진 table명만을 백업해야 했기 때문에 아래와 같은 명령어를 사용했다.

```bash
#!/bin/sh
sudo -u postgres pg_dump -d specific_database -t prefix_* > /opt/db_backup/db_backup_$(date +"%Y-%m-%d_%H:%M").sql
```

```bash
위 코드를 설명하자면 
1.sudo -u : 
postgres에 권한이 있는 사용자 postgres로 pg_dump라는 명령어를 작성하고
2. -d 특정 데이터베이스명 : 데이터 베이스를 선택
3. -t 테이블명 : 백업할 테이블 선택 \*는 문자열 와일드 카드로 어떤 문자가 나와도 된다. ex) prefix_a, prefix_b, prefix___c 등등
4. > : 이전까지의 명령으로 인한 산출물을 어디에 저장할지 쓴다
5. %(date + "%Y-%m-%d_%H:%M") : 현재 날짜와 시간을 작성하기 위한 date format 설정 방식
6. 위 코드가 돌아가면 /opt/db_bakup/ 디렉토리 안에 db_backip_2024-01-16_13:27.sql로 생성된다.
```

### 스케쥴링
---
이제 실행할 스크립트파일은 만들었지만 언제 돌릴지를 설정할 수 있어야 한다. 그렇게 하기 위한 linux의 기능이 **크론탭** 이다.

#### 크론탭
>[!info]
>리눅스는 크론탭, 윈도우는 스케줄러
>특정 시간에 작업을 하기 위한 명령어가 존재했다.

#### 크론탭 사용법
1. 크론탭 편집기 열기
```bash
crontab -e
```
2. 크론탭에 설정된 리스트 확인하기
```bash
crontab -l
```
3. 크론탭 지우기
```bash
crontab -r
```

#### 주기 설정
```
*         *         *        *        *
분(0-59) 시간(0-23) 일(1-31) 월(1-12) 요일(0-7) 0과 7은 일요일
```
예제
```bash
0 0 * * * /opt/test.sh
```
#### 크론 로깅
로그를 찍고 싶을 땐 로그를 작성할 파일 위치를 입력해주면 된다.
예제
```bash
0 0 * * * /opt/test.sh > /opt/test.log 2>&1
```

#### 방법
1. 먼저 crontab -e 를 쓴다. 
```bash
 crontab -e
```
2. 작성법에 따라 아래와 같이 작성했다
```bash
30 13 * * * /opt/shell_script_file_name.sh > /opt/db_backup.log 2>&1
```
3. 위와 같이 했는데 해당 스크립트가 실행되지 않았다. 이유는 권한이었다.
```bash
#권한 주기
chmod +x /opt/shell_script_file_name.sh
```

### 결과
---
결과로 db를 백업하는 시간을 줄일 수 있게 되었다.

#linux
#crontab
