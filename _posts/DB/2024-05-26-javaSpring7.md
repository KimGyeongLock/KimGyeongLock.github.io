---
layout: single
title: DTO / Mapper
toc: true
toc_sticky: true
categories: javaSpring
published: true
---

map type 쓰던걸 → dto로 바꿔보자

map은 다른 정보도 들어가기 때문에 메모리 손해

## 1. build.gradle에서 mybatis, swagger 관련 추가

```sql
//mybatis 사용
implementation 'org.mybatis.spring.boot:mybatis-spring-boot-starter:3.0.3' //3.0.2 => 3.0.3으로 상승!!
//swagger 사용!!!
implementation 'org.springdoc:springdoc-openapi-starter-webmvc-ui:2.0.2' //swagger 사용을 위함.
```

## 2. ~Application.java 파일에 **`@EnableJpaAutditing`** annotation 추가

- 데이터를 생성하거나 수정할 때, **누가, 언제**했는지를 알기 위해 DB에 표시
    - `createdAt` (생성일자)
    - `modifiedAt` (수정일자)
    - `createdBy` (생성자)
    - `modifiedBy` (수정자)
- 엔티티 객체가 생성이 되거나 변경이 되었을 때 자동으로 값을 등록할 수 있습니다.

## 3. Configuration 생성

- ChatGPT: Spring Framework와 MyBatis를 사용하여 데이터베이스와의 연결을 설정하는 구성 파일
- Spring ←→ MyBatis ←→ Database

```java
@Configuration
@MapperScan(basePackages = {"com.example.realspr.mapper"}, sqlSessionFactoryRef = "sqlSessionFactory")
public class MybatisConfig {
    @Bean(name = "sqlSessionFactory")
    public SqlSessionFactory sqlSessionFactory(@Qualifier("dataSource") DataSource dataSource) throws Exception {
        SqlSessionFactoryBean sqlSessionFactoryBean = new SqlSessionFactoryBean();
        sqlSessionFactoryBean.setDataSource(dataSource);
        sqlSessionFactoryBean.setTypeAliasesPackage("com.example.realspr.dto");
        sqlSessionFactoryBean.setMapperLocations(new PathMatchingResourcePatternResolver().getResources("classpath:/mapper/*.xml"));
        return sqlSessionFactoryBean.getObject();
    }
}
```

## 4. Entity에 createdAt, modifiedAt column 추가

- `@EntityListeners(AuditingEntityListener.class)` // 필수!

```java
@DateTimeFormat(iso = DateTimeFormat.ISO.DATE_TIME)
@CreatedDate
@Column(nullable = false, updatable = false)
protected LocalDateTime createdAt; // 생성일시

@DateTimeFormat(iso = DateTimeFormat.ISO.DATE_TIME)
@LastModifiedDate
@Column(nullable = false)
protected LocalDateTime modifiedAt; // 수정일시
```

## 5. 드디어 DTO 사용!

- **DTO(Data Transfer Object, 데이터 전송 객체)**
    - 전달하고 싶은 데이터만 담음
- **CreateDto** : create할때 필요한 Data Set
    - `toEntity` function
        - entity 생성 함수

```java
@Schema
@Getter
@Setter
@NoArgsConstructor
@AllArgsConstructor
public static class TbuserCreateDto { //create
    @Schema(description = "username", example = "이메일 주소")
    @NotNull
    @Email
    @NotEmpty
    @Size(max = 100)
    private String username;

    @Schema(description = "password", example = "비밀번호")
    @NotNull
    @NotEmpty
    @Size(max = 50)
    private String password;

    public Tbuser toEntity() { return Tbuser.of(username, password); }
}
```

- **AfterCreateDto**
    - id를 return
    - **Builder를 사용**

```java
@Schema
    @Getter
    @Setter
    @NoArgsConstructor
    @AllArgsConstructor
    **@Builder** // builder()
    public static class TbuserAfterCreateDto { //id를 돌려주는 역할
        @Schema(description = "id", example = "length32textnumber")
        private String id;
    }
```

- **UpdateDto**
- **SelectDto**

## 6. create 된 후

```java
public TbuserDto.TbuserAfterCreateDto toTbuserAfterCreateDto() {
    return TbuserDto.TbuserAfterCreateDto.builder().id(getId()).build();
}
```

- `builder()` 함수를 통해 셋팅하고자 하는 값을 셋팅하고 build()를 통해 빌더를 작동 시켜 **객체를 생성**
- builder 함수 사용 이유
    - **생성자 파라미터가 많을 경우 가독성이 좋지 않다.**
    - 빌더의 필드 이름으로 값을 설정하기 때문에 순서에 종속적이지 않다.

## 7. Mapper

- SQL 문을 사용해서 repository 보다 디테일한 조회
    - Query문을 많이 쓰는 조회문의 경우 Mapper를 사용
    - repository - create, update 처럼 간단한
- repository랑 비슷 (interface 사용)
    - mapper interface 생성

```java
public interface TbuserMapper {
    TbuserDto.TbuserSelectDto detail(String id);
    List<TbuserDto.TbuserSelectDto> list();
}
```

- Repository는 JPA가 해주지만, Mybatis 설정을 해줘야함
    - **xml** 파일 생성 및 연결

## 8. Service에서 Map → DTO 로 변경

```java
@Service
public interface TbuserService {
    public TbuserDto.TbuserAfterCreateDto create(TbuserDto.TbuserCreateDto param);
    public TbuserDto.TbuserAfterCreateDto update(TbuserDto.TbuserUpdateDto param);
    public TbuserDto.TbuserSelectDto get(String id);
}
```

- Service가 바꼈기 때문에 return type이 바뀜 그에 맞게 restController도 변경
- 컨트롤러에서 파라미터로 받을 때도 DTO
- 컨트롤러에서 서비스로 넘길 때도 DTO
- 서비스에서 다시 컨트롤러로 데이터 넘길 때도 DTO

