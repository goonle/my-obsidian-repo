> JPA(Java persistence API)
- Java 진영에서 ORM(Object_Realational Mapping) 기술 표준으로 사용되는 인터페이스 모음
- 자바 어플리케이션에서 관계형 DB를 사용하는 방식을 정의한 인터페이스
- 인터페이스이기 때문에 Hibernate, OpenJPA 등이 JPA를 구현함

### ORM
---
애플리케이션 Class와 RDB(Relational DataBase)의 테이블을 매핑한다는 뜻으로 기술적으로는 애플리케이션의 객체를 RDB 테이블에 자동으로 영속화 해주는 것이라고 보면 된다.

### JPA를 사용해야 하는 이유
---
- JPA는 반복적인 CRUD SQL을 처리해준다.
- 매핑된 관계를 이용하여 SQL을 생성하고 실행한다.
- 추가적으로 JPA로 구현이 어려운 쿼리문은 native SQL이라는 기능을 통해 직접 작성할 수 있다.

JPA를 사용하면서 얻을 수 있는 가장 큰 것은 SQL이 아닌 객체 중심으로 개발할 수 있다는 점이다.

객체의 관계에 따라 필요한 테이블에 저장할 수 있다.
(패러다임의 불일치 문제 해결)

#java 
#jpa
