---
layout: single
title: 전체 복습
toc: true
toc_sticky: true
categories: javaSpring
published: true
---

# 1. setting

- build.gradle
    
    ```sql
    dependencies {
    ...
    	 //domain (jpa)
    	 implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
    	 //db (mysql)
    	 runtimeOnly 'com.mysql:mysql-connector-j'
    	 //thymeleaf
    	 implementation 'org.springframework.boot:spring-boot-starter-thymeleaf'
    
    }
    ```
    
    - jpa 관련 코드와 mySQL 관련 코드 추가

- application.properties
    - [application.properties](http://application.properties) → application.yaml (이름 변경)
    직관적이고 편의를 위해
    - 연결한 Database의 정보를 담음 (url, username, password..)
    

# 2. Controller

- Controller
    - 페이지 이동을 위한 controller
    - 페이지(view)를 띄운다. ⇒ 프론트엔트 (실습용)
- RestController
    - 데이터 전송을 위한 controller ⇒ 백엔드

```sql
@GetMapping({"","/","/index"})
public String index() {
    return "index";
}
```

- `{"","/","/index"}`  : default page
    
    

```sql
@GetMapping("/{page}")
public String tbuser(@PathVariable("page") String pg) {
    return "tbuser/" + pg;
}
```

- `@PathVariable`  : /tbuser/insert와 /tbuser/detail 동시 사용
    
    path에 있는 변수("page")를 String pg로 넘겨줌
    

## 3. Domain

- DB table 만들기

```java
protected Tbuser(){}
private Tbuser(String username, String password, String name) {
    this.username = username;
    this.password = password;
    this.name = name;
}
public static Tbuser of(String username, String password) {
    return new Tbuser(username, password, "");
}
```

- Tbuser 생성자를 protected와 private로 막아놓음.

```java
@PrePersist
    public void onPrePersist() {
        this.id = UUID.randomUUID().toString().replace("-", "");
        this.deleted = "N";
    }
```

- `@PrePersist` : Entity가 영속화(생성)되기 직전에 실행되어야 하는 Entity의 메소드를 표시

## 4. Repository

```java
@Repository
public interface TbuserRepository extends JpaRepository<Tbuser, String> { //<entity, id(primary key의 자료형)>
}
```

## 5. Service

### Interface

```cpp
@Service
public interface TbuserService {
    public Map<String, Object> create(Map<String, Object> param);
}
```

- Interface를 사용하는 이유?
    
    뭘까
    

### Implement

```cpp
@Service
public class TbuserServiceImpl implements TbuserService {

    private TbuserRepository tbuserRepository;
    public TbuserServiceImpl(TbuserRepository tbuserRepository) {
        this.tbuserRepository = tbuserRepository;
    }

    public Map<String, Object> create(Map<String, Object> param) {
        Map<String, Object> resultMap = new HashMap<String, Object>();
        Tbuser tbuser = Tbuser.of(param.get("username")+"", param.get("password")+"");
        tbuserRepository.save(tbuser);
        resultMap.put("id", tbuser.getId());
        return resultMap;
    }
}
```

- `private TbuserRepository tbuserRepository;` : jpa repository 에서 save function을 사용
    
    생성자는 tbuserRepository를 초기화 하는 과정? (Dependency Injection)
    
    `param.get("username")+""` : Object type + “” → String type
    

## 6. Controller 마무리

```cpp
@RestController
@RequestMapping("/api/tbuser")
public class TbuserController {
    private TbuserService tbuserService;
    public TbuserController(TbuserService tbuserService) {
        this.tbuserService = tbuserService;
    }

    @PostMapping("")
    public Map<String, Object> create(@RequestBody Map<String, Object> param) { //DTO
        return tbuserService.create(param);
    }
}
```

## 7. HTML

```cpp
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Insert</title>
    <!--ajax 선언(정보 교환)-->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.7.1/jquery.min.js" integrity="sha512-v2CJ7UaYy4JwqLDIrZUI/4hqeoQieOmAZNXBeQyjo21dadnwR+8ZaIJVT8EE2iyI61OV8e6M8PP2/4hpQINQ/g==" crossorigin="anonymous" referrerpolicy="no-referrer"></script>
</head>
<body>
회원가입
아이디
<input type ="text" id="create_username"/>
비밀번호
<input type ="password" id="create_password"/>
<a href="javascript:create();">등록</a>
<!--javascript-->
<script>
    <!--using ajax-->
    function create() {
        $.ajax({
            url : '/api/tbuser', //TbuserController
            type : 'POST',
            contentType:'application/json; charset=utf-8',
            data : JSON.stringify({
                'username' : $('create_username').val(),
                'password' : $('create_password').val()
            }),
            beforeSend:function(){
                //
            },
            success : function(data){
                alert('등록되었습니다!');
            },
            error : function(request, status, error){
                alert("code:"+request.status+"\n"+"message:"+request.responseText+"\n"+"error:"+error);
            },
            complete:function(){
                //
            }
        });
    }
</script>
</body>
</html>
```

- **ajax**를 이용한 비동기 데이터 교환

## 궁금점

1. *application.yaml 코드는 외워야 하나??*
2. *아무 데이터도 넘겨주지도 받지도 않는 index.html의 경우 restController가 하는 것은 없어서 DefaultController에는 아무 코드도 없는 것인가?*
3. *thymeleaf의 기능?*
     * \"String으로 리턴을 하면 해당하는 파일명으로 찾아갈수 있게 도와줍니다.\"
     * \"return "index"; => index.html 파일로 페이지 이동하도록 / 없으면 불가\" (Controller)
5. *이전에는 `@RequestParam` 이 됐었는데 왜 `@RequestBody` 로 해야하나?*
     * 현재는 **GET** 일 경우에는 **RequestParam**으로 전달하고 이외의 방법(**PUT, POST** 등등)에서는 **RequestBody**로 전달
7. *왜 Tbuser 생성자를 protected와 private로 막아놓은건가? of를 쓰는 이유*
    * /"생성자는 디비에 저장하기 전에 해당 엔티티에 등록하려고 만드는 경우/"
    * /"정확히 필요한 파라미터를 확실히 설정/"
    * 큰 의미는 없다!
9. *`resultMap.put("id", tbuser.getId());` `getId` 는 내장함수?*
    * lombok의 @Getter annotation
