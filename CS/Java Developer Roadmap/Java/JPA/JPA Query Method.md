# JPA Query Method?
---
쉽게 말하자면 JPA의 가장 큰 장점인 쿼리를 직접 작성하지 않고 method의 이름만으로 쿼리처럼 사용하는 것인데
그 명명법에 대한 규칙이다.

특정 명명법을 사용해서 method명을 사용하면 쿼리를 작성하지 않고 데이터 조회가 가능하다.

[출처: docs.spring.io](https://docs.spring.io/spring-data/jpa/reference/jpa/query-methods.html)

### 예). Distinct, And
쿼리 문법에서 distinct는 중복된 데이터를 줄여주는 역할을 한다.
####  코드
```java
public interface UserRepository extends JpaRepository {
	findDistinctLastnameAndFirstname(String lastName, String firstName);
}
```

```sql
SELECT distinct \* from user_table where last_name = ?1 and first_name = ?2;
```

### 영어 뜯으로 이해하면 쉽다.
1. Distinct
2. And (and 조건)
3. Or (or 조건)
4. Is, Equals (=)
5. Between( 사이 )
6. LessThan (보다 작은)
7. LessThanEqual(보다 작거나 같은)
8. GreaterThan(보다 큰)
9. GreaterThanEqual(보다 크거나 같은)
10. After(  ~이후) 특정 시간(date) 이후
11. Before( ~이전)
12. IsNull, Null 
13. IsNotNull, NotNull
14. Like (like 연산)
15. NotLike
16. StrartingWith (sql로 따지면 condition like 'string%' )
17. EndWidth(sql로 따지면 condition like '%string')
18. Containing( condition like '%string%')
19. OrderBy( 순서)
20. Not (!=)
21.  In (where age in \[20,21,22\])
22. NotIn
23. True ( where married = true)
24. False
25. IgnoreCase( 조건과 값 모두 Upper Case 처리 후 비교)

#jpa #query
#method