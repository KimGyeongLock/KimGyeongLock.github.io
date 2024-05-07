---
layout: single
title: Spring3 (ajax)
toc: true
toc_sticky: true
categories: javaSpring
published: true
---

Controller → page 이동

RestController → 데이터 송/수신

- **ajax**
    - **비동기** 통신
    - 빠르게 동작하는 동적인 웹 페이지를 만들기 위한 개발 기법
    - jQuery 기능
    //웹에서 데이터를 보내고 api에서 데이터를 받아오는 기술들이 집약
    - [https://velog.io/@jeong_woo/Spring-Ajax-비동기-통신](https://velog.io/@jeong_woo/Spring-Ajax-%EB%B9%84%EB%8F%99%EA%B8%B0-%ED%86%B5%EC%8B%A0)

## Ex1)

### TbpostPageController

```java
@Controller //페이지 전환을 위한 컨트롤러!!
@RequestMapping("/tbpost")
public class TbpostPageController {
    @GetMapping("/abc")
    public String abc(){
        return "tbpost/def";
    }
}
```

- /tbpost/abc → tbpost/def

### TbpostRestController

```java
@RestController
@RequestMapping("/api/tbpost")
public class TbpostRestController {
    @GetMapping("/aaa")
    public Map<String, Object> aaa(@RequestParam Map<String, Object> map){
        Map<String, Object> resultMap = new HashMap<>();
        resultMap.put("hi", "hello");
				System.out.println("map : " + map);
        return resultMap;
    }
}
```

- /api/tbpost/aaa → resultMap
- resultMap ⇒ “hi”(key) : “hello”(value)

### tbpost/def.html

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
Hello! <b style="background-color:yellow;">def!!</b>INDEX!!!
<input type="text" id="input_title" />
<a href="javascript:aaaTest();">a태그 입니다.</a>
<button onclick="aaaTest()">버튼 입니다.</button>
<script>

    function aaaTest(){
        let input_title = $("#input_title").val(); //textfield에서 넣은 값
        //alert(1);
        $.ajax({
            url : '/api/tbpost/aaa',
            type : 'GET',
            dataType : "json",
            contentType:"application/json",
            data : {
                title : input_title
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

- 버튼이 눌렸을 때 aaaTest() 함수 실행
- ajax를 통해 get 방식으로 데이터를 받아오기
    - success: 성공시 받아온 data를 자바스크립트의 값을 JSON 문자열로 변환하여 알림
    - error
    - complete

### 결과

<img width="1043" alt="Untitled" src="https://github.com/KimGyeongLock/KimGyeongLock.github.io/assets/63464299/2f28811a-85aa-41b0-8c43-61b6f0423575">

## Ex2)

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
}
```

- /tbnotice/insert → tbnotice/insert
- /tbnotice/list → tbnotice/list

### TbnoticeRestController

```java
@RestController
@RequestMapping("/api/tbnotice")
public class TbnoticeRestController {

    List<Map<String, Object>> list_tbnotice = new ArrayList<>();

    @GetMapping("/create")
    public Map<String, Object> create(@RequestParam Map<String, Object> map){
        Map<String, Object> resultMap = new HashMap<>();
        System.out.println("map : " + map);
        System.out.println("title : " + map.get("title"));
        System.out.println("content : " + map.get("content"));
        int result_code = 500;
        int listSizeBefore = list_tbnotice.size();
        Map<String, Object> a_map = new HashMap<>();
        a_map.put("no", listSizeBefore);
        a_map.put("title", map.get("title") + "");
        a_map.put("content", map.get("content") + "");
        list_tbnotice.add(a_map);
        int listSizeAfter = list_tbnotice.size();
        if(listSizeAfter > listSizeBefore){ // 사이즈가 커졌다면 정상(데이터가 들어왔다)
            result_code = 200;
        }
        resultMap.put("resultCode", result_code);

        return resultMap;
    }

    @GetMapping("/list")
    public Map<String, Object> list(@RequestParam Map<String, Object> map){
        Map<String, Object> resultMap = new HashMap<>();
        System.out.println("map : " + map);

        /*List<Map<String, Object>> alist = new ArrayList<>();
        Map<String, Object> a_map = new HashMap<>();
        a_map.put("title", "제목1");
        a_map.put("content", "본문1");
        alist.add(a_map);*/

        resultMap.put("resultCode", "200");
        resultMap.put("list", list_tbnotice);

        return resultMap;
    }
}
```

- /api/tbnotice/create → resultMap
- /api/tbnotice/list → resultMap
- 연산 과정이 컨트롤러에서 실행되었지만 원래는 service에서 실행

### tbnotice/insert.html

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
공지사항 작성!!!
제목
<input type="text" id="input_title" />
내용
<input type="text" id="input_content" />
<a href="javascript:createTbnotice();">등록해줘요.</a>
<script>

    function createTbnotice(){
        let input_title = $("#input_title").val();
        let input_content = $("#input_content").val();
        //alert(1);
        $.ajax({
            url : '/api/tbnotice/create',
            type : 'GET',
            dataType : "json",
            contentType:"application/json",
            data : { //전송할 데이터?
                title : input_title
                ,content : input_content
            },
            beforeSend:function(){
                //
            },
            success : function(data){
                alert(JSON.stringify(data)); //{"resultCode":200}
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
<custom111 class="font_count" hellofriend="111222"></custom111>
<div id="div_list">

</div>
<script>
    let count = 0;
    // 동기식
    setInterval(function() {
        listTbnotice();
    }, 1000);

    function listTbnotice(){
        //alert(1);
        $.ajax({
            url : '/api/tbnotice/list',
            type : 'GET',
            dataType : "json",
            contentType:"application/json",
            data : null,
            beforeSend:function(){
                //
            },
            success : function(data){ //create의 데이터
                count++;
                $(".font_count").text(count);
                let a_list = data.list;
                for(let i=0;i<a_list.length;i++){
                    let checkObject = $(".list_tbnotice_" + a_list[i].no);
                    if($(checkObject).length == 0){ // 중복 제거
                        $("#div_list").append(
                            "<div class='list_tbnotice_"+a_list[i].no+"'>" + a_list[i].title + "//" + a_list[i].content + "</div>"
                        );
                    }
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

- setInterval을 통해 비동기식에서 동기식으로 1초마다 함수를 실행
    - 동기식 두가지 방식 -> 1. 몇초마다 계속 확인, 2. 소켓 여는 방식

### 결과 (공지사항 게시판)

<img width="1002" alt="Untitled 1" src="https://github.com/KimGyeongLock/KimGyeongLock.github.io/assets/63464299/6d8d8a08-a6f0-4f16-a706-20aea7c07422">

<img width="420" alt="Untitled 2" src="https://github.com/KimGyeongLock/KimGyeongLock.github.io/assets/63464299/3725b67c-5925-440b-8a5e-39b6b032a1e4">

- 제목과 내용 입력시 {”resultCode”: “200”}(정상송신)을 알림
- list에서 실시간으로 입력된 것을 확인(동기식)

## 궁금증

- insert.html에서 데이터를 입력했는데 list.html에서 data로 받아옴
