### 어떤 것을 위해 찾아보았는가?
---
세팅 테이블에서 조회기간에 대한 int 값을 받아서 현재 날짜에서 int 기간 전부터 현재까지의 데이터를 조회하여 간단한 통계 컬럼을 가지고 해당 row의 idx를 참조하여 다른 매핑테이블을 조회하여 다시 테이블을 조회하는 쿼리를 짜야했다. 그리고 다시 조회한 쿼리의 결과는 최종 row의 한 컬럼에 배열로 들어가야 했다.

풀어쓴 글을 정리하자면
1. setting_table.value = 10 (int4);
2. list_table의 조회기간은 register_dt >= 현재날짜 - (setting_table.value)일
3. map_table.target_idx = list_table.idx를 만족하는 map_table.list_idx를 구하기
4. map_table.idx로 다시 list_table로 조회하는데, 이는 결과 row의 new_list 컬럼에 배열로 담겨야 한다.

테이블을 그려보자면

| setting_table |                   |
| ------------- | ----------------- |
| value (int4)  | type_cd (varchar) |
| 30            | 'period'          |

| list_table   |       |       |       |       |                        |
| ------------ | ----- | ----- | ----- | ----- | ---------------------- |
| idx (serial) | a     | b     | c     | d     | register_dt(timestamp) |
| 1            | 'abc' | 'abb' | 'acc' | 'add' | 2024-03-13 00:00:00    |
| 2            | 'abc' | 'abb' | 'acc' | 'add' | 2024-03-13 00:00:00    |
| 3            | 'abc' | 'abb' | 'acc' | 'add' | 2024-03-13 00:00:00    |

| map_table |            |
| --------- | ---------- |
| list_idx  | target_idx |
| 1         | 1          |
| 2         | 1          |
| 3         | 1          |

### SQL 쿼리
--- --- ---

```sql
SELECT
	lt.idx,
	lt.a,
	lt.b,
	lt.c,
	lt.d,
	case 
		when MAX(lt2.list_idx) is null then '[]'::jsonb 
		else jsonb_agg( 
			jsonb_object('idx' , lt2.list_idx ,'a', lt2.a, 'b', lt2.b, 'c', lt2.c, 'd', lt2.d)
			) end as "new_list"
FROM
	list_table lt
LEFT JOIN
	setting_table st
ON
	st.type_cd = 'period' 
LEFT JOIN
	map_table mt
ON
	mt.target_idx = lt.idx
LEFT JOIN
	list_table lt2
ON
	lt2.idx = mt.list_idx
WHERE 
	lt.register_dt >= interval '1 day' * st.value
GROUP BY
	lt.idx, lt.a, lt.b, lt.c, lt.d
```

### 새로 배운 점
---
1. jsonb_agg
2. jsonb_object 
3. interval '1 day' \* int

#postgeSQL 
#sql