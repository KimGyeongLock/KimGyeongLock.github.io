---
layout: single
title: SNS(인스타) DB 설계
toc: true
toc_sticky: true
categories: javaSpring
published: true
---

## ERD

<img width="865" alt="Untitled" src="https://github.com/KimGyeongLock/KimGyeongLock.github.io/assets/63464299/18ae0acf-690d-4d45-9d8f-22f719ca9bc9">

---

## SQL

### \<유저 테이블\>

```sql
# tbuser CREATE
CREATE TABLE `tbuser` (
  `idx` varchar(200) COLLATE utf8_unicode_ci NOT NULL,
  `username` varchar(45) COLLATE utf8_unicode_ci DEFAULT NULL,
  `password` varchar(45) COLLATE utf8_unicode_ci DEFAULT NULL,
  `name` varchar(45) COLLATE utf8_unicode_ci DEFAULT NULL,
  `phone` varchar(45) COLLATE utf8_unicode_ci DEFAULT NULL,
  `gender` varchar(45) COLLATE utf8_unicode_ci DEFAULT NULL,
  PRIMARY KEY (`idx`),
  UNIQUE KEY `username_UNIQUE` (`username`) # UNIQUE ('username') 도 가능
);

INSERT INTO `tbuser` VALUES ('1','test1','1','홍길동','010','female'),('2','test2','2','james','011','male');
```

- **UNIQUE KEY unique_name (col1, col2)**
    - ```UNIQUE KEY `username_UNIQUE` (`username`)```    
    \: \`username\` = unique target      
        username_UNIQUE = 인덱스 이름, 해당 인덱스의 목적이나 유형을 나타내도록 지정
- Primary Key와 달리, **UNIQUE KEY**는 NULL 값을 포함할 수 있음
- ```UNIQUE(username)``` **\<대체가능\>**   
   \: 명시적인 이름이 없기 때문에 인덱스가 생성될 때 자동으로 생성된 이름이 사용됩니다. 이는 가독성과 유지보수 측면에서 제약 조건을 쉽게 식별하기 어려울 수 있습니다.
- ```UNIQUE KEY username_UNIQUE ('username')```     
   \: 명시적인 이름을 사용하기 때문에 해당 인덱스가 어떤 제약 조건을 나타내는지 쉽게 이해할 수 있습니다.
- ```COLLATE utf8_unicode_ci``` : 데이터 한글 인코딩 (안 써도 됨)

---

### \<게시물 테이블\>

```sql
# tbpost CREATE
CREATE TABLE `tbpost` (
  `idx` varchar(200) COLLATE utf8_unicode_ci NOT NULL,
  `title` varchar(45) COLLATE utf8_unicode_ci NOT NULL,
  `content` varchar(45) COLLATE utf8_unicode_ci DEFAULT NULL,
  `tbuser_idx` varchar(200) COLLATE utf8_unicode_ci NOT NULL,
  PRIMARY KEY (`idx`),
  KEY `fk_tbpost_tbuser_idx` (`tbuser_idx`),
  CONSTRAINT `fk_tbpost_tbuser_idx` FOREIGN KEY (`tbuser_idx`) REFERENCES `tbuser` (`idx`) ON DELETE CASCADE ON UPDATE CASCADE
);

INSERT INTO `tbpost` VALUES ('1','안녕','안녕하세요!!','1');
```

- **fk_tbpost_tbuser_idx** : index
- **CONSTRAINT**        
  \: 제약조건(constraint)이란 데이터의 무결성을 지키기 위해, 데이터를 입력받을 때 실행되는 검사 규칙
       index 활용
- ```ON DELETE CASCADE ON UPDATE CASCADE```     
\: 외래 키 제약 조건에서 사용되는 옵션      
     참조하는 테이블의 행이 삭제되거나 업데이트될 때의 동작
    - **```ON DELETE CASCADE```**: 이 옵션을 사용하면 외래 키가 참조하는 테이블의 행이 **삭제**될 때, **해당 행을 참조하는 모든 행도 자동으로 삭제**됩니다. 즉, 부모 테이블의 행이 삭제되면 자식 테이블의 관련된 모든 행도 함께 삭제됩니다. 이를 자식 행의 "CASCADE" 삭제라고 합니다.
    - **```ON UPDATE CASCADE```**: 이 옵션을 사용하면 외래 키가 참조하는 테이블의 기본 키(primary key)가 **업데이트**될 때, 해당 키를 참조하는 모든 외래 키 열도 **자동으로 업데이트**됩니다. 즉, 부모 테이블의 기본 키가 업데이트되면 자식 테이블에서도 해당 열을 참조하는 모든 값이 함께 업데이트됩니다.
- tbuser의 idx를 참고하여 tbuser_idx를 **FK**로 설정
    - tbuser : tbpost = 1 : ♾️

---

### \<picture? 사진첨부? 테이블\>

```sql
# tbpostpic CREATE
CREATE TABLE `tbpostpic` (
  `idx` varchar(200) COLLATE utf8_unicode_ci NOT NULL,
  `content` varchar(200) COLLATE utf8_unicode_ci DEFAULT NULL,
  `tbpost_idx` varchar(200) COLLATE utf8_unicode_ci NOT NULL,
  PRIMARY KEY (`idx`),
  KEY `fk_tbpostpic_tbpost_idx` (`tbpost_idx`),
  CONSTRAINT `fk_tbpostpic_tbpost_idx` FOREIGN KEY (`tbpost_idx`) REFERENCES `tbpost` (`idx`) ON DELETE CASCADE ON UPDATE CASCADE
);
```

- tbpost의 idx를 참고하여 tbpost_idx를 **FK**로 설정
    - tbpost : tbpostpic = 1 : ♾️

---

### \<게시글 좋아요 테이블\>

```sql
# tbpostlike CREATE
CREATE TABLE `tbpostlike` (
  `idx` varchar(200) COLLATE utf8_unicode_ci NOT NULL,
  `tbpost_idx` varchar(200) COLLATE utf8_unicode_ci NOT NULL,
  `tbuser_idx` varchar(200) COLLATE utf8_unicode_ci NOT NULL,
  PRIMARY KEY (`idx`),
  UNIQUE KEY `uq_tbpostlike_tbuser_tbpost_idx` (`tbpost_idx`,`tbuser_idx`),
  KEY `fk_tbpostlike_tbpost_idx` (`tbpost_idx`),
  KEY `fk_tbpostlike_tbuser_idx` (`tbuser_idx`),
  CONSTRAINT `fk_tbpostlike_tbpost_idx` FOREIGN KEY (`tbpost_idx`) REFERENCES `tbpost` (`idx`) ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT `fk_tbpostlike_tbuser_idx` FOREIGN KEY (`tbuser_idx`) REFERENCES `tbuser` (`idx`) ON DELETE CASCADE ON UPDATE CASCADE
);
```

- tbpost의 idx를 참고하여 tbpost_idx를 **FK**로 설정
    - tbpost : tbpostlike = 1 : ♾️
- tbuser의 idx를 참고하여 tbuser_idx를 **FK**로 설정
    - tbuser : tbpostlike = 1 : ♾️
- ```UNIQUE KEY `uq_tbpostlike_tbuser_tbpost_idx` (`tbpost_idx`,`tbuser_idx`)```
    - 한 포스트에 하나만 좋아요 하기 위해 FK 두개를 묶어서 Unique

---

### \<게시글 댓글 테이블\>

```sql
# tbpostcmt CREATE
CREATE TABLE `tbpostcmt` (
  `idx` varchar(200) COLLATE utf8_unicode_ci NOT NULL,
  `content` varchar(200) COLLATE utf8_unicode_ci NOT NULL,
  `tbpost_idx` varchar(200) COLLATE utf8_unicode_ci NOT NULL,
  `tbuser_idx` varchar(200) COLLATE utf8_unicode_ci NOT NULL,
  PRIMARY KEY (`idx`),
  KEY `fk_tbpostcmt_tbpost_idx` (`tbpost_idx`),
  KEY `fk_tbpostcmt_tbuser_idx` (`tbuser_idx`),
  CONSTRAINT `fk_tbpostcmt_tbpost_idx` FOREIGN KEY (`tbpost_idx`) REFERENCES `tbpost` (`idx`) ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT `fk_tbpostcmt_tbuser_idx` FOREIGN KEY (`tbuser_idx`) REFERENCES `tbuser` (`idx`) ON DELETE CASCADE ON UPDATE CASCADE
);
```

- tbpost의 idx를 참고하여 tbpost_idx를 **FK**로 설정
    - tbpost : tbpostcmt = 1 : ♾️
- tbuser의 idx를 참고하여 tbuser_idx를 **FK**로 설정
    - tbuser : tbpostcmt = 1 : ♾️

---

### \<팔로우 테이블\>

```sql
# tbfollow CREATE
CREATE TABLE `tbfollow` (
  `idx` varchar(200) COLLATE utf8_unicode_ci NOT NULL,
  `from_tbuser_idx` varchar(200) COLLATE utf8_unicode_ci NOT NULL,
  `to_tbuser_idx` varchar(200) COLLATE utf8_unicode_ci NOT NULL,
  PRIMARY KEY (`idx`),
  KEY `fk_tbfollow_from_tbuser_idx` (`from_tbuser_idx`),
  KEY `fk_tbfollow_to_tbuser_idx` (`to_tbuser_idx`),
  CONSTRAINT `fk_tbfollow_from_tbuser_idx` FOREIGN KEY (`from_tbuser_idx`) REFERENCES `tbuser` (`idx`) ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT `fk_tbfollow_to_tbuser_idx` FOREIGN KEY (`to_tbuser_idx`) REFERENCES `tbuser` (`idx`) ON DELETE CASCADE ON UPDATE CASCADE
);

INSERT INTO `tbfollow` VALUES ('1','1','2'),('2','2','1');
```

- tbuser의 idx를 참고하여 from_tbuser_idx를 **FK**로 설정 (누가)
    - tbuser : tbfollow = 1 : ♾️
- tbuser의 idx를 참고하여 to_tbuser_idx를 **FK**로 설정     (누구를 팔로우 할 것인가?)
    - tbuser : tbfollow = 1 : ♾️

## Example

```sql
SELECT tbuser.name, tbuser.gender, tbpost.title, tbpost.content
FROM tbuser, tbpost
WHERE username = 'test1';
```

<img width="509" alt="Untitled 1" src="https://github.com/KimGyeongLock/KimGyeongLock.github.io/assets/63464299/0f798661-1f06-44db-9182-b02662f40ae8">
