# Camp Connect

### π’ μΊ νμ₯ μ°ΎκΈ° μ΄λ €μ°μ¨μ£ ? μ ν¬ μΊ ν μ»€λ₯νΈκ° μ°κ²° μμΌλλ¦¬κ² μ΅λλ€!

π μ¬μ΄νΈ μ£Όμ: https://bit.ly/2YYBOXm

πΊ λ°λͺ¨ μμ: https://www.youtube.com/watch?v=tvhFhO4n3OU

π κ°λ° κΈ°κ°: 10/11 ~ 10/16

π¨π»βπ€βπ¨π» Front: μ€μ§μ  & μ΄κ²½μ

π¨π»βπ€βπ¨π» Back: κΉνμ & νμ¬ν

---

π― κ°λ° λͺ©ν: 

1. μλ‘ λ€λ₯Έ κ°λ°νκ²½μμμ μ°λ(CORS) 
2. νμκ°μ & Springμμ JWT λ°©μμ λ‘κ·ΈμΈ 
3. μΊ νμ₯ μΉ΄νκ³ λ¦¬ νν°λ§ 
4. μΊ νμ₯ λ¦¬λ·° CRUD κΈ°λ₯
5. μΊ νμ₯ μμ½ κΈ°λ₯
6. λ§μ΄νμ΄μ§ μμ½ νν© μ‘°ν

---

β Tech Stack

| Stack     | Front        | Back                         |
| --------- | ------------ | ---------------------------- |
| Framework | React, Redux | Spring boot, Spring Security |
| Library   | Axios, Immer |                              |
| Database  |              | MySQL                        |
| Deploy    | S3           | AWS                          |

---

β API

![image](https://user-images.githubusercontent.com/76515226/137482416-85a2a2a9-3e35-4ba9-a705-1ae68508e113.png)

![image](https://user-images.githubusercontent.com/76515226/137482503-46e59404-3a44-44ba-a576-c8e85e9f6bb6.png)

---

β ERD

![image](https://user-images.githubusercontent.com/76515226/137482671-07892edd-687b-48c8-8e27-eb050952906b.png)

---

β νΈλ¬λΈμν

#### 1. CORS

νλ‘ νΈμ€λμ λ°±μ€λκ° μ²μμΌλ‘ νμνλ μλ¦¬μκ³  κ°κ° λ€λ₯Έ νκ²½μμ κ°λ°μ νλ€λ³΄λ CORS λ¬Έμ κ° λ°μνλ€.

μλ‘ μΆμ²κ° λ€λ₯Έ μΉ μ νλ¦¬μΌμ΄μμμ μμμ κ³΅μ νλ©° νλ‘μ νΈλ₯Ό μ§ννκ³  νλ‘ νΈμλμ λ°±μλμ μΆμ²κ° λ¬λΌ CORSμλ¬κ° λ°μν κ²μ νμΈνλ€

λΈλΌμ°μ λ λ³΄μμμ μ΄μ λ‘ κ΅μ°¨ μΆμ² HTTPμμ²­μ μ ννκΈ°μ μ΄λ₯Ό ν΄κ²°νκΈ° μν΄μ  λ°±μλμ CORSκ΄λ ¨ μ€μ μ ν΄μ£Όμ΄μΌ νλ€λ κ²μ λ°°μ λ€.

μ΄μ ν΄κ²°λ°©λ²μΌλ‘ νμ¬ BackEnd νλ‘μ νΈμλ μΈμ¦λΆλΆμ μ€νλ§ μνλ¦¬ν°λ‘ μ²λ¦¬νκ³  μμκ³  ν΄λΉ κ²½μ° κ°λ¨νκ² μ€νλ§ μνλ¦¬ν° μ€μ μΌλ‘ CORSνμ©μ ν μκ° μμλ€.

```java
@Configuration
public class WebConfig implements WebMvcConfigurer {
    @Override
    public void addCorsMappings(CorsRegistry registry) {
        registry.addMapping("/**")
                .allowedOrigins("http://54.180.132.5/","http://localhost:3000")
               
                .allowedMethods("POST","GET","PUT","DELETE","HEAD","OPTIONS") 
                
                .allowCredentials(true);
    }
```
WebConfig ν΄λμ€ μμ± ν λͺ¨λ  κ²½λ‘μ λν΄ corsλ₯Ό μ μ©νκΈ° μν΄ addMapping("/**")λ₯Ό μ¬μ©νλ€. 

λν .allowedMethodsμ ν΅ν΄ ν΄λΌμ΄μΈνΈμμ μμ²­νλ λ©μλ λ²μ(GET,POST λ±λ±)λ₯Ό μ νκ³  ν΄λΌμ΄μΈνΈμμ μΏ ν€λ₯Ό λ°κΈ° μν΄ allowCredentials(true)μ μ¬μ©νλ€.

μ λ°©ν₯ μλ²μμ μμ²­μ μ£Όκ³  λ°κΈ° μν΄ .allowedOriginsμ νλ‘ νΈμ λ°±μλμ μ£Όμλ₯Ό μΆκ°νλ©° μ€νλ§μ€μ μ νλ€.

```java
public class WebSecurityConfig extends WebSecurityConfigurerAdapter {

    private final JwtTokenProvider jwtTokenProvider;

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        **http.cors();**
        http.csrf().disable()
                .csrf().disable()
                .sessionManagement().sessionCreationPolicy(SessionCreationPolicy.STATELESS) 
                .and()
                ...(μ€λ΅)
```
μ€νλ§ μνλ¦¬ν°μμλ WebSecurityConfigurerAdapterλ₯Ό μμνλ ν΄λμ€λ₯Ό νλ λ§λ  ν configureλ₯Ό μ¬μ μ(corsλ©μλ μ¬μ©)νλ μ€μ μ ν΄μ£Όμλ€.

#### 2. JWT

ν ν°μ μ΄μ©νκ² λλ©΄ μΏ ν€μ ν ν°μ λ΄μ headerμ μ€μ΄μ λ³΄λ΄κ² λλ€, frontμμλ μ΄ ν ν°μ λ°μμ λ‘κ·ΈμΈ μ λ³΄λ₯Ό μ΄μ©νμ¬ λ‘κ·ΈμΈμ νκ³  λ§€ κΆνμ΄ νμν μμ²­λ§λ€ ν ν°μ λ΄μμ κ°μ΄ λ³΄λ΄κ² λλ€.

```java
// JwtTokenProvider

private String secretKey = "μν¬λ¦Ώ ν€";
// νλ‘ νΈμ μΌμΉμμΌμΌ νλ ν ν° μ ν¨μκ°
private Long toemValidTime = 24 * 60 * 60 * 1000L;

// screckeyλ₯Ό base64λ‘ μΈμ½λ©
@PostConstruct
protected void init() {
    secretKey = Base64.getEncoder().encodeToString(secretKey.getBytes());
}

// JWT ν ν° μμ±
public String createToken(String userPk) {
    Claims claims = Jwts.claims().setSubject(userPk); // JWT payload μ μ μ₯λλ μ λ³΄λ¨μ

    Date now = new Date();

    return Jwts.builder()
        .setClaims(claims) // μ λ³΄ μ μ₯
        .setIssuedAt(now) // ν ν° λ°ν μκ° μ λ³΄
        .setExpiration(new Date(now.getTime() + tokenValidTime)) // set Expire Time
        .signWith(SignatureAlgorithm.HS256, secretKey)  // μ¬μ©ν  μνΈν μκ³ λ¦¬μ¦κ³Ό
        // signature μ λ€μ΄κ° secretκ° μΈν
        .compact();
}

// ν ν°μμ νμ μ λ³΄ μΆμΆ
public String getUserPk(String token) {
    return Jwts.parser().setSigningKey(secretKey).parseClaimsJws(token).getBody().getSubject();
}

// JWT ν ν°μμ μΈμ¦ μ λ³΄ μ‘°ν
public Authentication getAuthentication(String token) {
    UserDetails userDetails = userDetailsService.loadUserByUsername(this.getUserPk(token));
    return new UsernamePasswordAuthenticationToken(userDetails, "", userDetails.getAuthorities());
}

// Requestμ headerμμ ν ν° κ° κ°μ Έμ€κΈ° (keyκ°μ νλ‘ νΈμ μΌμΉμμΌμΌ νλ€)
public String resolveToken(HttpServletRequest request) {
    return request.getHeader("X-AUTH-TOKEN");
}

// ν ν°μ μ ν¨μ± + λ§λ£μΌμ νμΈ
public boolean validateToken(String jwtToken) {
    try {
        Jws<Claims> claims = Jwts.parser().setSigningKey(secretKey).parseClaimsJws(jwtToken);
        System.out.println(claims); // JWT ν ν°(ν΄λΌμ΄μΈνΈμμ λ³΄λΈ)μ΄ μ λ€μ΄μ€λμ§ κ²μ¦
        return !claims.getBody().getExpiration().before(new Date()); // expireμκ°μ΄ λμ§ μμλ€λ©΄ True
    } catch (Exception e) {
        return false;
    }
}
```

