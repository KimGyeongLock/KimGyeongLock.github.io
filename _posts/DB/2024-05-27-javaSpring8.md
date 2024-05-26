---
layout: single
title: MyBatis
toc: true
toc_sticky: true
categories: javaSpring
published: true
---

MyBatis를 통해 더 디테일한 조회를 만들어보자!

## 1. DTO 에 list 추가

- 검색이라 꼭 포함할 필요 없으니까 Not NULL 까지 할 필요 없다.

```java
@Schema
@Getter
@Setter
@NoArgsConstructor
@AllArgsConstructor
public static class ListReqDto {
    @Schema(description = "username", example = "")
    private String username;
    @Schema(description = "name", example = "")
    private String name;
    @Schema(description = "nick", example = "")
    private String nick;
    @Schema(description = "phone", example = "")
    private String phone;
}
```

## 2. RestController 에 list 추가

```java
@GetMapping("/list")
public ResponseEntity<List<TbuserDto.SelectResDto>> list(@Valid TbuserDto.ListReqDto param) {
    return ResponseEntity.status(HttpStatus.OK).body(tbuserService.list(param));
}
```

- tbuserService.list(param) : list 함수가 필요하다.
- TbuserService, TbuserServiceImpl 에 list 함수 추가

```java
public List<TbuserDto.SelectResDto> list(TbuserDto.ListReqDto param);
```

```java
public List<TbuserDto.SelectResDto> list(TbuserDto.ListReqDto param) {
    List<TbuserDto.SelectResDto> list = tbuserMapper.list(param);
    List<TbuserDto.SelectResDto> newlist = new ArrayList<>();
    for(TbuserDto.SelectResDto tbuserSelectDto : newlist) {
        newlist.add(get(tbuserSelectDto.getId()));
    }
    return newlist;
}
```

## 3. xml 에 list 추가

```java
<select id="list" parameterType="hashMap" resultType="com.example.realspr.dto.TbuserDto$SelectResDto">
        SELECT tbuser.id
        FROM tbuser
        WHERE tbuser.id is not null
        <if test = "username != null and username != ''">AND tbuser.username = #{username}</if>
        <if test = "name != null and name !=''">AND tbuser.name LIKE CONCAT('%', #{name}, '%')</if>
        <if test = "nick != null and nick !=''">AND tbuser.nick LIKE CONCAT('%', #{nick}, '%')</if>
        <if test = "phone != null and phone !=''">AND tbuser.phone = #{phone}</if>
    </select>
```

## 4. list.html (with handlebars)

- **CDN(Content Delivery Network)** 을 통해 **handlebars.js** 사용
    - **cdn** : 콘텐츠를 가능한 한 빠르고, 저렴하고, 신뢰할 수 있고, 안전하게 전송하기 위해 상호 연결된 서버의 네트워크
    - **handlebars** : {{}} (bracket)을 이용하여 데이터 표현, list를 front로 보여줄때 많이 사용
    js parsing 객체 있으면 html로 만들어줌

```html
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.7.1/jquery.min.js" integrity="sha512-v2CJ7UaYy4JwqLDIrZUI/4hqeoQieOmAZNXBeQyjo21dadnwR+8ZaIJVT8EE2iyI61OV8e6M8PP2/4hpQINQ/g==" crossorigin="anonymous" referrerpolicy="no-referrer"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/handlebars.js/4.7.8/handlebars.min.js" integrity="sha512-E1dSFxg+wsfJ4HKjutk/WaCzK7S2wv1POn1RRPGh8ZK+ag9l244Vqxji3r6wgz9YBf6+vhQEYJZpSjqWFPg9gg==" crossorigin="anonymous" referrerpolicy="no-referrer"></script>
</head>
<body>
<script id="list_info_tbuser" type="text/x-handlebars-template">
    {{#resultData_tbuser}}
    <div>
        {{createdAt}} / {{modifiedAt}}
        {{username}} // {{name}} // {{nick}}
    </div>
    {{/resultData_tbuser}}
</script>
<script type="text/javascript">
    var list_info_tbuser = $("#list_info_tbuser").html();
    var list_info_tbuser_template = Handlebars.compile(list_info_tbuser);
</script>
```

## 결과
<img width="1440" alt="Untitled" src="https://github.com/KimGyeongLock/KimGyeongLock.github.io/assets/63464299/b122a44f-8db6-4884-a7f7-ca8e92e953f3">

## 궁금증

[http://localhost:8080/api/tbuser/list?username=”dd”](http://localhost:8080/api/tbuser/list?username=%E2%80%9Ddd%E2%80%9D) : 이거 왜 안되지
