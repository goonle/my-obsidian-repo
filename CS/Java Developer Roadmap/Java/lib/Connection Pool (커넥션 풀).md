### 커넥션 풀을 공부하는 이유
---
커넥션 풀에 대해 들어봤다. DB연결에 대한 용어이고 불필요한 DB연결과 해제를 제거하여 성능(속도)를 높이기 위함정도로 알고 있었다. 하지만 커넥션 풀이 정확이 어떤 것인지, 설정에는 무엇이 있는지 알기 위함이다.

### 예제 코드
---
일단 아래의 코드를 보자. 해당 내용은 "JSP 2.3 웹프로그래밍 기초부터 중급까지"의 chapter14 Connection Pool을 보고 작성한다.

```java
package jdbc;

import java.sql.DriverManager;
import java.util.Properties;

import javax.servlet.ServeltException;
import javax.servlet.http.HttpSevlet;

import org.apache.commons.dbcp2.BasicDataSource;
import org.apache.commons.dbcp2.BasicDataSourceFactory;
import org.apache.commons.dbcp2.ConnectionFactory;
import org.apache.commons.dbcp2.DriverManagerConnectionFactory;
import org.apache.commons.dbcp2.PoolableConnection;
import org.apache.commons.dbcp2.PoolableConnectionFactory;
import org.apache.commons.dbcp2.PoolingDriver;
import org.apache.commons.pool2.ObjectPool;
import org.apache.commons.pool2.impl.GenericObjectPool;
import org.apache.commons.pool2.impl.GenericObjectPoolConfig;

public class DBCPInit extends HttpServlet {

    @Override
    public void init() throws ServletException {
        loadJDBCDriver();
        initConnectionPool();
    }

    private void loadJDBCDriver(){
        try {
            Class.forName("com.mysql.jdbc.Driver");
        }catch (ClassNotFoundException ex){
            throw new RuntimeException("fail to load JDBC Driver", ex);
        }
    }
    //initConnectionPool
    public void initConnecitonPool(){
        try{
            String jdbcUrl = 
                "jdbc:mysql://localhost:3306/chapter?useUnicode=true&characterEncoding=utf8";
            String username = "test";
            String pw = "testpw";
            //create connection 
            ConnectionFactory connFac = new DriverManagerConnectionFactory(jdbcUrl, username, pw);
            PoolableConnectionFactory poolableConnFac = new PoolableConnectionFactory(connFac, null);

            poolableConnFac.setValidationQuery("select 1");
            //setting connection pool
            GenericObjectPoolConfig poolConfig = new GenericObjectPoolConfig();
            poolConfig.setTimeBetweenEvictionRunsMillis(1000L * 60L * 5L); //5 minutes
            poolConfig.setTestWhileIdle(true);
            poolConfig.setMinIdle(4);   //guess maximum 20minites wait
            poolConfig.setMaxTotal(50); //guess maximun 50 connections

            GenericObjectPool<PoolableConnection> connectionPool = new GenericObjectPool<>(poolableConnFac, poolConfig);
            poolableConnFac.setPool(connectionPool);

            Class.forName("org.apache.commons.dbcp2.PoolingDriver");
            PoolingDriver driver = (PoolingDriver) DriverManager.getDriver("jdbc:apache:commons:dbcp:");
            driver.registerPool("chap14", connectionPool);
        }catch(Exception e){
            throw new RuntimeException(e);
        }
    }
}

```
### 코드를 보고난 후
---
코드를 보면 GenericObjectPoolCofig를 통해 세팅을 하는 것을 알 수 있다. 
1. setTimeBetweenEvictionRunsMillis:  매서드의 이름과 받는 인자를 보면 밀리세턴드를 의미하는 int를 받아 시간을 설정하는 것으로 보인다.
2. setTestWhileIdle : Idle(유휴시간) 동안 테스트를 하는 설정인 것으로 보인다.
3. setMinIdle : 최소 유휴뭔가를 설정하는 것으로 보이고
4. setMaxTotal :  최대 설정을 하는 것으로 보인다.

그럼 정확히 알아보자

| Method                 | Explaination                                                    | word     | meaning |
| ---------------------- | --------------------------------------------------------------- | -------- | ------- |
| setTimeBetweenEviction | 풀에 있는 유휴 커넥션 검사 주기를 설정한다. 양수가 아니면 검사하지 않는다. 단위는 밀리 세컨드이다.       | eviction | 축출      |
| setTestWhileIdle       | true일 경우, 유휴 커넥션이 유효한지 검사한다.                                    | idle     | 유휴시간    |
| setMinIdle             | 커넥션 풀이 유지할 최소 유휴 커넥션 개수를 지정한다.  maxIdle보다 크면 maxIdle 값이 최소가 된다. |          |         |
| setMaxTotal            | 풀이 관리하는 커넥션의 최대 개수를 설정한다. 음수면 제한이 없다.                           |          |         |

위가 설명이며 천천히 알아보기 전에 잘 모르는 용어에 대해 먼저 살펴본다.
##### 1.eviction
축출이라는 뜻이며 오래되었거나 상대적으로 사용하지 않으며 크기가 너무 큰 데이터를 제거하는 것을 뜻한다.
[출처](https://docs.jboss.org/jbossclustering/hibernate-caching/3.3/en-US/html/eviction.html)
위와 같은 의미로 setTimeBetweenEviction은 축출(제거)하기 전에 검사할 시간(주기)를 세팅하는 것으로 볼 수 있다.
##### 2. 유휴시간
한국말인데 유추가 어렵다. (유휴, 遊休 : 쓰지 않고 놀림) [출처:oxford languages](https://languages.oup.com/google-dictionary-ko/)
컴퓨터 용어로는 "컴퓨터 시스템이 사용가능한 상태이나 실제적인 작업이 없는 시간" [출처:TTA정보통신용어사전](https://terms.tta.or.kr/dictionary/searchList.do?searchContent=conts01&searchRange=all&listCount=10&listPage=1&orderby=KOR_SUBJECT&reFlag=N&orderbyOption=TRUE&conts01WhereSet=&firstWordVal=&firstWord=N&word_seq=&div_big_cd_in=51&div_big_cd=&searchTerm=%EC%9C%A0%ED%9C%B4%20%EC%8B%9C%EA%B0%84&searchCate=field)
이라고 한다. setTestWhileIdle은 유휴시간 동안 테스트를 할지 설정하는 것으로,
오랫동안 사용하지 않는 커넥션은 연결이 끊기게 되는데 이 커넥션을 사용할 경우 에러가 난다. 그렇기 때문에 커넥션 풀에서 연결이 끊긴 커넥션은 제거를 해줘야 에러를 방지 할 수 있다. 그렇기 때문에 유휴상태인 커넥션이 현재 연결이 되어있는지 체크할 것인지를 설정하는 매서드이다.

나머지 매서드에 대한 설명이다.
##### 3. setMinIdle
최소 유휴상태를 유지하는 커넥션 개수를 설정하는 것으로, 만약 0으로 설정이 되어있다면 커넥션 풀에 최소 0개가 유지되어 DB연결을 다시 해야하는 일이 발생하는데 이럴 경우 연결하는데 소요되는 시간 때문에 성능이 느려질 수 있으며 0이 계속유지한다면 커넥션 풀을 사용하는 의미가 퇴색된다. 그래서 보통 CPU 코어의 2배수로 설정을 한다.

##### 4. setMaxTotal
DBMS가 수용할 수 있는 connection의 개수를 넘어가면 전체성능에 안좋은 영향을 끼친다고 한다.

#java 
#connection 
#pool
