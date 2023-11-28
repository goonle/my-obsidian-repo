
dblink는 서로다른 database의 테이블을 조회하여 조인 문 혹은 view를 생성하는데 사용하는 기능입니다.

### postgresql
---
##### 사용방법

```sql
	Select {column_list}
	from
		dblink('dbname={remote_database}', 'SELECT * from {remote_table}')
```

위와 같이 같은 postgres 서버에 있는 다른 데이터베이스를 참조 할 수 있습니다.

##### 유의사항
1. 바로 실행하면, 실행되지 않습니다. 왜냐하면 해당 기능을 사용하기 위한 명령어를 치지 않았기 때문입니다.
	-  create extension dblink;
2. dblink 안의 sql 문에서는 \*(아스터리스크)를 사용할 수 있지만 밖에서 참조할 때는 사용할 수 없습니다.
	- [postgresql: docs - dblink](https://www.postgresql.org/docs/current/contrib-dblink-function.html)의 *Return Value*를 살펴보면 어떤 쿼리든 dblink를 사용하면 record형식으로 반환되며 이 말은 PostgreSQL은 우리가 원하는 것을 알 수 없다고 합니다. 그렇기에 컬럼명을 적어줄 것을 명시하고 있습니다.

#postgreSQL
#dblink
