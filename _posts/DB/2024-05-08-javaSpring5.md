---
layout: single
title: DB 연동 (jpa)
toc: true
toc_sticky: true
categories: javaSpring
published: true
---

## 테이블 생성
### Tbnotice

```java
@Getter
@ToString(callSuper = true)
@Table(indexes = {
        @Index(columnList = "title")
        ,@Index(columnList = "createdAt")
        ,@Index(columnList = "modifiedAt")
})
@Entity
public class Tbnotice {

    @Id //PK를 뜻하는것!! 이거 없으면 엔티티 에러남!
    private String id;

    @Setter
    protected String deleted;

    @DateTimeFormat(iso = DateTimeFormat.ISO.DATE_TIME)
    @CreatedDate
    protected LocalDateTime createdAt; // 생성일시

    @DateTimeFormat(iso = DateTimeFormat.ISO.DATE_TIME)
    @LastModifiedDate
    protected LocalDateTime modifiedAt; // 수정일시

    @Setter @Column(nullable = false) private String title; // 제목
    @Setter @Column(nullable = false, length=2000000) @Lob private String content; // 본문

    protected Tbnotice(){}
    private Tbnotice(String id, String title, String content) {
        this.id = id;
        this.title = title;
        this.content = content;
    }
    public static Tbnotice of(String id, String title, String content) {
        return new Tbnotice(id, title, content);
    }
}
```

- Database에 테이블(Tbnotice)을 생성
- 왜 ***of?***

## Repository with JPA
### TbnoticeRepository

```java
public interface TbnoticeRepository extends JpaRepository<Tbnotice, String> { //<entity, id>
}
```

- **JPA**
    - save, findById, findAll 같은 내장함수를 선언하지 않아도 jpa가 지원

## Service
### TbnoticeService

```java
@Service
public class TbnoticeService {

    private final TbnoticeRepository tbnoticeRepository;
    public TbnoticeService(
            TbnoticeRepository tbnoticeRepository
    ) {
        this.tbnoticeRepository = tbnoticeRepository;
    }

    public int create(Map<String, Object> map){
        String id = UUID.randomUUID() + "";
        id = id.replaceAll("-", "");
//        Tbnotice tbnotice = new Tbnotice() // 이거 안됨 protected랑 private 막아놔서 of로 씀
        Tbnotice tbnotice = Tbnotice.of(id,
                map.get("title") + "",map.get("content") + "");
        tbnoticeRepository.save(tbnotice);
        return 0;
    }

    public Tbnotice read(String id){
        Tbnotice tbnotice = tbnoticeRepository.findById(id)
                .orElseThrow(() -> new RuntimeException(""));
        return tbnotice;
    }
    public List<Tbnotice> list(){
        List<Tbnotice> list = tbnoticeRepository.findAll();
        return list;
    }
}
```

- Service = 연산 역할 = 함수 선언
- 생성자
- create
- read
    - **`.orElseThrow(() -> new RuntimeException(""))`**: **`findById`** 메서드의 반환 타입은 **`Optional`**입니다. 이것은 결과가 없을 수도 있다는 것을 의미합니다. 따라서 **`Optional`** 객체의 **`orElseThrow`** 메서드를 호출하여 해당 값이 존재하지 않을 경우 예외를 발생시킵니다. 여기서는 **`RuntimeException`**을 발생시키고 있습니다. 빈 문자열 **`""`**은 예외 메시지를 나타냅니다.
- list

## Controller
### TbnoticeRestController

```java
@RestController
@RequestMapping("/api/tbnotice")
public class TbnoticeRestController {

    private final TbnoticeService tbnoticeService;
    public TbnoticeRestController(
            TbnoticeService tbnoticeService
    ) {
        this.tbnoticeService = tbnoticeService;
    }

    @GetMapping("/create")
    public Map<String, Object> create(@RequestParam Map<String, Object> map){
        Map<String, Object> resultMap = new HashMap<>();
        System.out.println("map : " + map);
        System.out.println("title : " + map.get("title"));
        System.out.println("content : " + map.get("content"));
        tbnoticeService.create(map);
        return resultMap;
    }

    @GetMapping("/read")
    public Tbnotice read(@RequestParam String id) { 
			  return tbnoticeService.read(id); 
		}

    @GetMapping("/list")
    public List<Tbnotice> list(){
        return tbnoticeService.list();
    }
}

```

- 데이터 수신
- @RequestParam Map<String, Object> map ← /tbnotice/insert.html 에서 데이터 전송
    
    ```jsx
    function createTbnotice(){
        let input_title = $("#input_title").val();
        let input_content = $("#input_content").val();
        //alert(1);
        $.ajax({
            url : **'/api/tbnotice/create'**,
    ```
    
- @RequestParam String id ← /tbnotice/read.html 에서 데이터 전송
- list는 데이터 전송 x
    
    ```java
    $.ajax({
                url : '/api/tbnotice/list',
                type : 'GET',
                dataType : "json",
                contentType:"application/json",
                ****data **: null,**
    ```
    
- 데이터 송신
    
    ```java
    success : function(data){
                    ~~~
    },
    ```
    

## 결과

<img width="978" alt="Untitled" src="https://github.com/KimGyeongLock/KimGyeongLock.github.io/assets/63464299/f7d90e60-5e1d-4135-9554-143b355a0532">

<img width="1091" alt="Untitled 1" src="https://github.com/KimGyeongLock/KimGyeongLock.github.io/assets/63464299/928d0e92-7ecf-45fc-8913-7772598a34e4">

<img width="420" alt="Untitled 2" src="https://github.com/KimGyeongLock/KimGyeongLock.github.io/assets/63464299/024120b5-b1ad-4655-ad99-a17b19a1b17a">

- 데이터에 잘 들어오는 것을 확인할 수 있음

## Bonus

### TbnoticePageController

```java
@Controller
@RequestMapping("/tbnotice")
public class TbnoticePageController {
    @GetMapping("/insert")
    public String insert(){
        return "tbnotice/insert";
    }

    @GetMapping("/list")
    public String list(){
        return "tbnotice/list";
    }

    @GetMapping("/detail")
    public String detail(){
        return "tbnotice/detail";
    } // detail 페이지 추가
}
```

### tbnotice/list.html

```html
<!---->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.7.1/jquery.min.js" integrity="sha512-v2CJ7UaYy4JwqLDIrZUI/4hqeoQieOmAZNXBeQyjo21dadnwR+8ZaIJVT8EE2iyI61OV8e6M8PP2/4hpQINQ/g==" crossorigin="anonymous" referrerpolicy="no-referrer"></script>
</head>
<body>
공지사항 목록
<a href="/tbnotice/insert">등록하러 가기</a>
<div id="div_list">

</div>
<script>
    /*let count = 0;
    setInterval(function() {
        listTbnotice();
    }, 1000);
*/
    listTbnotice();
    function listTbnotice(){
        $.ajax({
            url : '/api/tbnotice/list',
            type : 'GET',
            dataType : "json",
            contentType:"application/json",
            data : null,
            beforeSend:function(){
                //
            },
            success : function(data){
                let a_list = data;
                //alert(JSON.stringify(data));
                for(let i=0;i<a_list.length;i++){
                    $("#div_list").append(
                        "<div class='list_tbnotice_"+a_list[i].id+"'>" +a_list[i].id +"//"+ a_list[i].title + "//" + a_list[i].content + "</div>"
                    );
                }
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

### tbnotice/detail.html

```html
<!---->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.7.1/jquery.min.js" integrity="sha512-v2CJ7UaYy4JwqLDIrZUI/4hqeoQieOmAZNXBeQyjo21dadnwR+8ZaIJVT8EE2iyI61OV8e6M8PP2/4hpQINQ/g==" crossorigin="anonymous" referrerpolicy="no-referrer"></script>
</head>
<body>
공지사항 상세보기!!!
ID :
<input type="text" id="input_id" />
<div class="div_tbnotice_title">-</div>
<div class="div_tbnotice_content">-</div>
<a href="javascript:readTbnotice();">조회해줘요.</a>
<script>

    function readTbnotice(){
        let input_id = $("#input_id").val();
        $.ajax({
            url : '/api/tbnotice/read',
            type : 'GET',
            dataType : "json",
            contentType:"application/json",
            data : {
                id : input_id
            },
            beforeSend:function(){
                //
            },
            success : function(data){
                alert(JSON.stringify(data));
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

<img width="987" alt="Untitled 3" src="https://github.com/KimGyeongLock/KimGyeongLock.github.io/assets/63464299/8016a732-75ec-4422-9684-2217e3c43139">
