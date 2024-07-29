### 사용법
##### 1. comma 사용
```sql
select
	a.a, a.b, a.c
from
	table_a a, period_table pt
where
	a.register_date >= (current_date - interval pt.days)
```

##### 2. 명시
```sql
select
	a.a, a.b, a.c
from
	table_a a
cross join 
	period_table pt
where
	a.register_date >= (current_date - interval pt.days)
```

CROSS JOIN은 두 테이블 사이에 가능한 모든 조합을 만든다.

### 주의사항
```sql
select
	a.a, a.b, a.c
from
	table_a a, period_table pt
join
	table_b b
on
	b.a = a.a
```

위 쿼리처럼 조인 테이블이 2개 이상일 경우 에러를 발생한다 그때는 명시하여 사용해야 한다.