[돌아가기](./README.md)

# SQL

DB 정보를 사용하도록 지원하는 언어

→ 모든 DBMS에 통용됨 (대소문자 구분 x)

### DML (Data Manipulation Language)

DB 테이블에서 새로운 행을 입력하거나, 기존 행의 변경 및 제거를 수행

- INSERT

    ```sql
    insert into 테이블이름 (col1, col2, ...)
    values (val1, val2, ...);
    ```

- UPDATE

    ```sql
    update 테이블이름
    set col1 = val1;
    ```

- DELETE

    ```sql
    delete from 테이블이름
    [where col=val];
    ```

### DDL (Data Definition Language)

데이터 구조 생성, 변경, 제거를 수행

- CREATE

    **기본 디비 생성**

    ```sql
    create database 데이터베이스이름;
    ```

    **이모지 문자(utf8mb4)까지 처리하는 DB (utfmb3: 다국어처리)**

    ```sql
    create database 데이터베이스이름
    default character set utf8mb4 collate utf8mb4_general_ci;
    ```

    **table 생성**

    ```sql
    use 데이터베이스이름;
    create table 테이블이름 (
    	idx  INT  NOT NULL AUTO_INCREMENT,
    	userid VARCHAR(16) NOT NULL,
    	userpwd VARCHAR(16)
    	PRIMARY KEY (idx)
    ) ENCHINE=InnoDB DEFAULT CHARSET=utf8;
    ```

- ALTER

    ```sql
    alter database 데이터베이스이름 default character set utf8mb4 collate utf8mb4_general_ci; 
    ```

- DROP

    ```sql
    drop database 데이터베이스이름;

    use 데이터베이스이름; // db 사용
    ```

- RENAME

    ```sql
    rename table old to new;
    ```

### DML 명령 수행의 버전 변경을 관리

- COMMIT
- ROLLBACK

### DCL (Data Control Language)

DB와 그 구조에 대한 접근 권한 제공, 제거를 수행

- GRANT
- REVOKE
