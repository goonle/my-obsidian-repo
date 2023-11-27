[출처 : graphql.org : code ](https://graphql.org/code/)
GraphQL은 쿼리 언어다. 그렇기에 특정언어로만 구성되는 것이 아니다.
하지만 React와 로고가 비슷한데 이는 React의 창시자가 페이스북의 엔지니어이며 GraphQL은 Facebook에서 만들었기 때문이다.

이 때문에 GraphQL의 예제가 js파일로 구성되어있는 예제를 많이 찾아볼 수 있게 되어있다. 

그래서 GraphQL은 JS 특화된 쿼리 언어라고 생각했지만 공식 사이트에서 각 언어별 예제를 작성해두었다.

![[Pasted image 20231122081904.png]]

```java
import graphql.ExecutionResult;
import graphql.GraphQL;
import graphql.schema.GraphQLSchema;
import graphql.schema.StaticDataFetcher;
import graphql.schema.idl.RuntimeWiring;
import graphql.schema.idl.SchemaGenerator;
import graphql.schema.idl.SchemaParser;
import graphql.schema.idl.TypeDefinitionRegistry;
import static graphql.schema.idl.RuntimeWiring.newRuntimeWiring;

public class HelloWorld {

    public static void main(String[] args) {
        String schema = "type Query{hello: String}";

        SchemaParser schemaParser = new SchemaParser();

        TypeDefinitionRegistry typeDefinitionRegistry = schemaParser.parse(schema);

        RuntimeWiring runtimeWiring = newRuntimeWiring()

                .type("Query", builder -> builder.dataFetcher("hello", new StaticDataFetcher("world")))

                .build();

        SchemaGenerator schemaGenerator = new SchemaGenerator();

        GraphQLSchema graphQLSchema = schemaGenerator.makeExecutableSchema(typeDefinitionRegistry, runtimeWiring);

        GraphQL build = GraphQL.newGraphQL(graphQLSchema).build();

        ExecutionResult executionResult = build.execute("{hello}");

        System.out.println(executionResult.getData().toString());

        // Prints: {hello=world}

    }

}
```


### GraphQL Spring Boot
---
GraphQL 스프링 부트는 어떤 어플리케이션도 GraphQL 서버로 변환시키며 다음과 같은 기능을 포함합니다.
- GraphQL 자바 툴의 도움으로 스키마 기반 API를 사용합니다.
- 선택적으로 GraphQL-Java Annotations을 도움으로 어노테이션 기반 스ㅜ키마를 사용할 수 있습니다.
- 스키마 사전 검수와 쿼리 디버깅을 위해 GraphiQL 툴을 임베드할 수 있습니다.
- 스키마 사전 검수와 쿼리 디버깅을 위해 GraphQL Playground 툴을 임베드할 수 있습니다.
- 당신의 GraphQL API를 상호작용 가능한 그래프로 표현하기 위해 GraphQL Voyager 툴을 임베드할 수 있습니다.

#java-developer-roadmap 
#clientAPI
#graphQL 