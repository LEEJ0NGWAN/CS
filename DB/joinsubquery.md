[돌아가기](./README.md)

# View

베이스 테이블을 바탕으로 만들 수 있는 논리(가상) 테이블

실제 데이터를 가지고 있지 않지만, 뷰를 통한 조작이 실제 베이스 테이블에 반영될 수 있다

### 사용 목적

1. 보안
2. SQL 재사용 (SQL 가독성 높임)

### 뷰 수정

뷰는 DDL의 `ALTER` 를 사용할 수 없다

→ `CREATE OR REPLACE VIEW 뷰이름` 사용

```sql
create or replace view v_emp_name
as select ename from emp;
```

### mysql if

`if (조건문, 참리턴, 거짓리턴) alias` 형태를 가진다

**기존 sql case 구문**

```sql
case substr(주민번호,8,1)
	when '1' then '남'
	when '3' then '남'
	else	'여'
end as "성별"
```

**mysql if**

```sql
if (substr(주민번호,8,1)='1' or substr(주민번호,8,1)='3','남','여')
```

### mysql with rollup

`with rollup` 을 이용하여 그룹핑 합계를 계산할 수 있다

`group by 조건` 뒤에 붙어 조건에 대한 합계 또한 계산해 준다.

**기존 union all**

```sql
select deptno, sum(sal)
from emp
group by deptno
union all
select null, sum(sal)
from emp;
```

**with rollup**

```sql
select deptno, sum(sal)
from emp
group by deptno with rollup;
```

### grouping

`grouping(칼럼)` 형태로 처리된 해당 칼럼의 null값이 grouping 처리에 의해 생긴 null이면 1 아니면 0 반환

# join

연관된 데이터를 한번에 sync 후 맞춰 가져옴

→ 조회하고 싶은 데이터가 2개 이상의 테이블에 나뉘었을 때 사용

### equi-join

동등 비교 조건 (=)

### nonequi-join

동등 비교가 아니고, 크거자 작은 경우 join을 수행하는 조건

```sql
select ename, sal, grade
from emp, salgrade 
where emp.sal between losal and hisal;
```

### inner join

조인 조건에 부합하는 레코드(조인이 가능한 레코드) 출력

```sql
select ename, dname
from emp join dept on emp.deptno=dept.deptno
```

### outer join

조인 조건에 부합하는 레코드뿐만 아니라 부합하지 않는 레코드(기준 테이블 기준)도 포함하여 출력

```sql
select ename, dname
from emp left join dept on emp.deptno=dept.deptno
```

### self join

자신과 자신을 조인하는 형태(계층형 테이블의 경우)

```sql
select e.ename, d.ename
from emp e join emp d on e.mgr=d.ename
```

### cross join

두 테이블의 모든 가능한 조인을 전부 처리한 형태의 결과 (곱집합)

→ 조인 조건을 명시하지 않음 (조건 명시하면 오류 발생)

```sql
select *
from emp cross join dept;
```

### natural join

자연스러운 조인

(조인 조건을 명시하지 않고, natural join 구문 사용: 두 테이블의 공통 칼럼 이용하여 조인)

```sql
select *
from emp natural join dept;
```

## join ~ using

두 테이블의 공통 칼럼 동등 비교 조인

```sql
select empno, ename, dname
from emp join dept using(deptno);
```

## semi join

exists 연산자 사용

**관리자인 직원을 조회하는 예제**

```sql
select e.empno, e.ename, '관리자'
from emp e
where exists ( select 1 from emp where e.empno=mgr)
```

# Index (색인)

레코드 조회 성능을 높이기 위한 기법

- 레코드 수가 많고, 중복 값이 적을 때 유용
- 수정이 빈번한 경우 인덱스 불리

### 복합 컬럼 형태 인덱스

인덱스 생성 시 컬럼 한개만 이용하는 것이 아니라 여러개의 칼럼을 이용

→ 관련 컬럼 1개 찾을 때, 여러 컬럼 찾을 때 모두 복합 컬럼 인덱스 사용 가능

# Btree (Balanced Tree)

각 인덱스의 값 또한 순차로 검색하는데 성능 개선을 위해 사용된 자료구조

### branch

Btree root의 바로 밑에 위치한 자손으로, 리프노드(인덱스 값들을 나타내는 노드)에 빠르게 접근하기 위해 각 브랜치가 가지고 있는 자손 리프노드의 인덱스 값의 범위를 나타낸다

→ 인덱스 값 검색 시, 브랜치를 통해 1차적으로 크고 빠르게 범위를 검색할 수 있다.

### leaf node

실제 인덱스의 값을 가지고 있는 노드

# subquery

어떤 sql 문 안에 포함, 중첩, 내포된 query (select 쿼리)

- 조회 레코드 수에 따라

    단일행 서브쿼리, 다중행 서브쿼리로 나눈다

- 조회 칼럼 수에 따라

    단일열 서브쿼리, 다중열 서브쿼리로 나눈다

- subquery가 mainquery 값과 연관되어 처리되는지에 따라
    - 상호연관(correlated) 서브쿼리: mainquery가 먼저 실행되고 값이 subquery로 전달

    ```sql
    select *
    from emp e
    where e.sal = (select max(sal) from emp where deptno=e.deptno);
    ```

    - 비상호연관(uncorrelated) 서브쿼리: subquery가 먼저 실행되고 mainquery로 값을 전달

### subquery 포함 가능한 질의문

- select

    select col, (select ~) ⇒ scalar subquery (단일행, 단일열 서브쿼리)

    from (select ~) ⇒ inline view

    where xx (select ~) ⇒ 조건 비교 값

- insert values
- update set
- create table

# where 비교 구문

- in (= any)
- not in
- > any : 최소
- > all : 최대
- < any
- < all
