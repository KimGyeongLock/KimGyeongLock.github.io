---
layout: single
title: Paging
toc: true
toc_sticky: true
categories: javaSpring
published: true
---

# AuditingFields 생성

- 공통 필드 추출
- 공통으로 사용하는 column들을 재사용
- `@MappedSuperclass`  : Entity에서 공통된 필드를 사용할 때 Base Entity에 정의

Auditing은 Audit(감시하다)의 뜻 그대로 Entity를 보고있다가 DB에 저장하거나 업데이트를 하는 경우 생성일자, 생성자, 수정일자, 수정자 등 중요한 메타데이터를 자동으로 데이터베이스에 반영해주는 기능이다.

출처: [https://velog.io/@yun8565/JPA-Auditing-정리](https://velog.io/@yun8565/JPA-Auditing-%EC%A0%95%EB%A6%AC)

---

# Paging

- 전체 게시물의 갯수를 다 계산한 다음 몇개씩 자를지 정함
    - ⇒ 비효율적이다.
    - 게시물이 많이 안된다면 사용, 너무 많으면 시간이 너무 오래 걸림

## plist.html 페이지 생성

- cdn에서 **jquery**와 **handlebars** 사용

```jsx
<script src="https://cdnjs.cloudflare.com/ajax/libs/handlebars.js/4.7.8/handlebars.min.js" integrity="sha512-E1dSFxg+wsfJ4HKjutk/WaCzK7S2wv1POn1RRPGh8ZK+ag9l244Vqxji3r6wgz9YBf6+vhQEYJZpSjqWFPg9gg==" crossorigin="anonymous" referrerpolicy="no-referrer"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.7.1/jquery.min.js" integrity="sha512-v2CJ7UaYy4JwqLDIrZUI/4hqeoQieOmAZNXBeQyjo21dadnwR+8ZaIJVT8EE2iyI61OV8e6M8PP2/4hpQINQ/g==" crossorigin="anonymous" referrerpolicy="no-referrer"></script>
```

- handlebars를 통해 list가 보여주는 Front를 표현
- perpage: 한번에 볼 페이지 수 , callpage: 내가 보고 싶은 페이지
- orderway: 검색 방향, orderby: 검색 기준

## TbpostMapper.java 필요한 함수 선언 (interface)

```java
List<TbpostDto.SelectResDto> pagedList(TbpostDto.PagedListReqDto param);
int pagedListCount(TbpostDto.PagedListReqDto param);
```

- pagedList : 요청된 게시물의 list return
- pagedListCount : 전체 게시물의 갯수 return

## TbpostMapper.xml

- TbpostMapper.java에서 선언한 함수들을 implement.

```xml
<select id="pagedList" parameterType="hashMap" resultType="com.example.realspr.dto.TbpostDto$SelectResDto">
    SELECT tbpost.id
    FROM tbpost
    WHERE tbpost.id is not null
    <if test = "deleted != null and deleted != ''">AND tbpost.deleted = #{deleted}</if>
    <if test = "title != null and title !=''">AND tbpost.title LIKE CONCAT('%', #{title}, '%')</if>
    <if test = "cate != null and cate != ''">AND tbpost.cate = #{cate}</if>
    <if test = "orderby == 'created_at'">ORDER BY tbpost.created_at</if>
    <if test = "orderby == 'title'">ORDER BY tbpost.title</if>
    <if test = "orderway == 'asc'">ASC</if>
    <if test = "orderway == 'desc'">DESC</if>
    LIMIT #{calllimit}, #{perpage}
</select>
<select id="pagedListCount" parameterType="hashMap" resultType="Integer">
    SELECT count(tbpost.id) as listsize
    FROM tbpost
    WHERE tbpost.id is not null
    <if test = "deleted != null and deleted != ''">AND tbpost.deleted = #{deleted}</if>
    <if test = "title != null and title !=''">AND tbpost.title LIKE CONCAT('%', #{title}, '%')</if>
    <if test = "cate != null and cate != ''">AND tbpost.cate = #{cate}</if>
</select>
```

- *왜 created_at으로 표시되지*
- *cate 빼도됨?*
- LIMIT #{calllimit}, #{perpage} : (calllimit)에서 시작하여 (perpage) 만큼의 행을 조회

## TbpostDto

- PagedListReqDto : list 요청 시 입력 받는 변수들의 Dto
- PagedListResDto : list 출력 시 필요한 Dto

```java
@Schema
@Getter
@Setter
@NoArgsConstructor
@AllArgsConstructor
public static class PagedListReqDto {
    @Schema(description = "deleted", example = "")
    private String deleted;
    @Schema(description = "title", example = "")
    private String title;
    @Schema(description = "cate", example = "")
    private String cate;

    @Schema(description = "callpage", example = "")
    private int callpage;
    @Schema(description = "calllimit", example = "")
    private int calllimit;
    @Schema(description = "perpage", example="")
    private int perpage;
    @Schema(description = "orderby", example="")
    private String orderby;
    @Schema(description = "orderway", example="")
    private String orderway;
}

@Schema
@Getter
@Setter
@NoArgsConstructor
@AllArgsConstructor
public static class PageListResDto {
    @Schema(description = "요청 페이지", example = "1")
    private int callpage;
    @Schema(description = "마지막 페이지", example = "100")
    private int lastpage;
    @Schema(description = "한번 조회할 갯수", example = "100")
    private int perpage;
    @Schema(description = "전체 갯수", example = "1")
    private int listsize;

    @Schema(description = "리스트", example = "상세정보가 담긴 리스트")
    private List<SelectResDto> list;
}
```

- *cate 는 html에서 받지 않는다 빼도 되지 않을까?*
- *calllimit은?*

## TbpostServiceImpl

```java
public TbpostDto.PagedListResDto pagedlist(TbpostDto.PagedListReqDto param) {
    TbpostDto.PagedListResDto returnDto = new TbpostDto.PagedListResDto();

    //총 갯수
    int count = tbpostMapper.pagedListCount(param);

    int perpage = param.getPerpage();
    //고객이 실제로 요청한 콜페이지
    int callpage = param.getCallpage();
    int lastpage = (int) count / perpage;
    if(count % perpage != 0){
        lastpage++;
    }
    //고객이 요청한 페이지의 첫번째 자료의 순번
    int calllimit = (callpage - 1) * perpage;
    param.setCalllimit(calllimit);
    param.setCallpage(callpage);
    List<TbpostDto.SelectResDto> pagedlist = tbpostMapper.pagedList(param);
    List<TbpostDto.SelectResDto> newlist = new ArrayList<>();
    for(TbpostDto.SelectResDto tbpostSelectDto : pagedlist) {
        newlist.add(get(tbpostSelectDto.getId()));
    }
    
    //PageListResDto
    returnDto.setLastpage(lastpage);
    returnDto.setPerpage(perpage);
    returnDto.setCallpage(callpage);
    returnDto.setListsize(count);

    returnDto.setList(newlist);
    
    return returnDto;
}
```

- lastpage : 전체 페이지 / 페이지당 게시물 갯수 = 총 페이지의 수 (올림해줘야함)
- calllimit(고객이 요청한 페이지의 첫번째 자료의 순번) : 요청한 페이지 * 페이지당 게시물 갯수
    - 0번 부터 9번, 10번~19번

## 결과

![8120b233-cedb-4262-8388-cc2c4a8ed3d0](https://github.com/KimGyeongLock/KimGyeongLock.github.io/assets/63464299/0279f5af-c9c0-4fd5-a1c5-25bc7e9f049f)


![6524d4fd-4977-4e14-83fa-843825736368](https://github.com/KimGyeongLock/KimGyeongLock.github.io/assets/63464299/a0996e14-77b9-4a88-9173-e921dd9b8a4d)


- 한 페이지에 2개의 게시물을 볼 수 있을 때 1페이지에는 2개가 출력, 2페이지에는 1개가 출력됨
