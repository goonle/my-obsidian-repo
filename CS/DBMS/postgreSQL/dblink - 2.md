

### DbLink + View 실사용을 위한 테스트 케이스
---
>[?] 원본 테이블 컬럼이 삭제되었을 때 View가 동작하는지?
-  에러 발생

> [?] 컬럼명이 변경 될 경우 View가 동작하나?
- 상관없이 동작함.

> [?] 원본 테이블 컬럼의 자료형이 변경되면 View 동작하나?
- 자료형이 int에서 varchar로 바뀌었을 때, 형변환이 가능한 값이라면 괜찮지만 형변환 할 수 없는 값일 경우, 에러 발생

> [?] 원본 테이블 컬럼이 추가되면 View 에도 적용할 수 있나?
-  에러 발생

> [?] 원본 테이블명이 변경되면 View에도 적용할 수 있나?
-  오류: "public.sew_test" 이름의 릴레이션(relation)이 없습니다

>[?] 꼭 같은 DB서버 안에 있어야 DbLink를 사용할 수 있나
- 가능한 것 같습니다.
```sql
SELECT dblink_connect('연결명', 'hostaddr=원격DB주소 port=원격DB포트 dbname=사용할DB이름 user=사용할DB계정 password=계정비밀번호')
```
- [참조 : 곰탱푸닷컴 - PostgreSQL의 dblink로 원격 Database 사용하기](https://www.bearpooh.com/145)

>[?] 원본 테이블의 코멘트 변경 시 VIew에도 코멘트를 수정할 수 있나?
- 따로 수정은 가능하나 자동수정은 안됩니다.

>[?] - DB계정에 VIEW 권한이 있어야지 볼 수 있는건가? 계정생성시 기본값이 VIEW 권한을 포함하고 있는가?
-  dblink를 사용할 계정은 SUPERUSER 권한이 필요하다고 합니다.

#dblink 
#postgreSQL 
