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

### JPA의 중요 컨셉
---
#### 1. 엔티티 매니저
- **엔티티**는 데이터 베이스의 테이블과 매핑되는 객체다.
- **엔티티 매니저**는 엔티티를 관리해 DB와 APP 사이에서 객체를 생성 및 변경,삭제하는 역할을 한다.
- **엔티티 매니저 팩토리**는 엔티티 매니저를 만든다.
- 스프링에서는 엔티티 매니저를 하나만 생성해 @PersistenceContext 혹은 @Autowired를 통해 사용할 수 있다.

#### 2. 영속성 컨텍스트
- 엔티티를 관리하는 가상의 공간

- ##### 속성
	- 1차 캐시 : 캐시에 조회한 데이터가 있으면 DB조회 없이 값을 반환한다.
	- 쓰기 지연 : 트랜젝션을 커밋하기 전까지 쿼리를 모아 한번에 처리한다.
	- 변경 감지 : 트랜젝션 커밋시 데이터를 비교하여 변경을 DB에 적용한다.
	- 지연 로딩 : 필요할 때 데이터를 조회한다.

#### 3. 엔티티의 상태
- 분리상태 : 영속성 컨텍스트가 관리 중 x
- 관리상태
- 비영속 상태
- 삭제된 상태

```java
public class EntityManagerTest {
	@Autowired
	EntityManager em;

	public void example(){
		//비영속 상태
		Member member = new Member(1L, "홍길동");

		em.persist(member)//관리 상태
		em.detach(member) //분리 상태
		em.remove(member) //삭제된 상태
	
	}
}
```

### 스프링 데이터와 JPA
엔티티 매니저를 통한 엔티티 상태를 직접 관리하는 것은 신경써야 할 부분이 많다.
Spring Data는 개발 로직에 집중할 수 있도록 DB 사용 기능을 클래스 레벨에서 추상화했다. 

다른 DB에 맞춤기능을 제공한다.

JPA를 위해 Spring Data JPA가 있다.

#### 스프링 데이터 JPA
PagingAndSortingRepository를 상속받아 JpaRepository 인터페이스를 만들었다. 
```java
@Repository
public interface MemberRepository extends JpaRepository<Member, Long> {

}
```
받는 인수(제네릭)에는 <엔티티이름, 엔티티 기본키의 타입>을 입력하면 기본 CRUD 메서드를 사용할 수 있다.



#java 
#jpa
