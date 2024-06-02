>[!info] CSRF란?
>CSRF(Cross site request forgery)는 웹사이트의 취약점을 이용하여 이용자가 의도하지 않은 요청을 통한 공격을 의미합니다.

간단한 해결책으로는 CSRF Token 정보를 Header에 포함시켜 서버에 요청을 시도하는 것입니다.
아래 코드에서 antMatchers()에 ant 패턴으로 작성된 규칙에 맞는  url만을 허가합니다.

```java
@Configuration
@EnableWebSecurity
public class SecurityConfig {

    @Autowired
    private JwtTokenFilter jwtTokenFilter;

    @Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        http
            .csrf()
                .csrfTokenRepository(csrfTokenRepository())
                .and()
            .sessionManagement().sessionCreationPolicy(SessionCreationPolicy.STATELESS)
            .and()
            .authorizeHttpRequests()
            .antMatchers("/api/v1/user/login", "/api/v1/user/join", "/api/v1/user/csrf").permitAll()
            .anyRequest().authenticated();
	}

	@Bean
    public CsrfTokenRepository csrfTokenRepository() {
        HttpSessionCsrfTokenRepository repository = new HttpSessionCsrfTokenRepository();
        repository.setHeaderName("X-CSRF-TOKEN");
        return repository;
    }
}
```

#csrf
