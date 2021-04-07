[돌아가기](./README.md)

# File: 데이터 저장

→ 구조적 Data 관리, 공유 및 트랜잭션이 어려움

⇒ DB 등장

Java App ← Framework(JPA, Hibernate, ...) → DBMS → DataFile (how)

### Table 구성요소

- view : 논리테이블, 가상테이블 (보안, 가독)
- function
- index

# DataBase

데이터 집합

# SQL

- DDL

    create, drop, alter

- DML

    insert, update, delete

- DCL

    grant, revoke

- TCL

    rollback, commit, savepoint

- DQL

    select

### 시스템 튜닝

1. SQL 튜닝

    → Table 설계

# 제약조건

데이터 무결성 보장을 위한 제약사항

- PK : 레코드 중복 방지 (2개 이상 칼럼 가능)
- FK : 창조의 결함을 방지
- UNIQUE : 중복 방지, NULL 가능
- NOT NULL : 생략 불가능
- CHECK : 주어진 범주 안의 값 안 갖도록
- default : 데이터 저장 시 기본값 부여

# insert, update, delete

### insert

```sql
insert into 테이블이름 [(col1, col2, ... , colN)]
values ( , , ... , );
```

### update

```sql
update 테이블이름
set col1=?, col2=?, ...
[where 조건]
```

### delete

```sql
delete from 테이블이름
[where 조건]
```

# select

```sql
select col...
from 테이블이름, 뷰이름
where 레코드 필터링 조건
group by 레코드 그룹핑 조건
having 그룹핑 결과 필터링 조건
order by 정렬기준
```
