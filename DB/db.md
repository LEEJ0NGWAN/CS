[돌아가기](./README.md)

# 데이터 무결성

데이터의 정확성, 일관성, 유효성을 전부 유지하고 있는 성질

- 데이터 정확성

    데이터가 정확한 값을 가지고 있음을 나타내는 성질

- 데이터 일관성

    해당 데이터에 관심을 가지는 모든 사용자가 일관된 값을 볼 수 있음을 나타내는 성질

- 데이터 유효성

    스키마에서 설정한 도메인을 위반하지 않는지와 같은 데이터의 유효성을 나타내는 성질

### 무결성 제약조건

DB에 저장된 데이터의 정확성(일관성)을 보장하기 위해, 유효하지 않은 데이터를 방지하는 제약 조건

## 무결성 종류

- 개체 무결성

    개체의 기본키는 빈 값을 허용하지 않는다

- 참조 무결성

    참조 관계의 두 테이블에 존재하는 데이터는 일관된 값을 가진다

- 도메인 무결성

    각 테이블 필드에는 올바른 값을 입력했는지 검증한다

- 고유 무결성

    어떤 필드의 유니크 조건에 대해, 각 레코드는 유일한 값을 가진다

- NULL 무결성

    어떤 필드에 NULL을 허용하지 않는 경우에 대해 NULL을 입력하지 않는다

- 키 무결성

    모든 릴레이션은 최소한 하나의 키가 존재해야한다

## 무결성 유지 이유

→ 현실 세계의 실제 값과 데이터로 가공하여 저장한 DB 데이터 사이의 괴리감을 없애고 신뢰를 제공하기 위해

# 트랜잭션

DB를 조작(SQL로 DB에 접근)하기 위해 수행하는 최소 작업 단위

## ACID

- Atomicity (원자성)

    트랜잭션의 연산은 정상적으로 DB에 완전 반영이 되던가, 전혀 반영이 되지 않는다 (모 아니면 도)

- Consistency (일관성)

    트랜잭션이 성공적으로 완료되면 DB 상태는 일관성있게 변환된다

- Isolation (독립성)

    수행되고 있는 트랜잭션이 완전히 완료되기 전까지 다른 트랜잭션에서 관련 데이터를 참조할 수 없다

- Durability (영속성)

    성공적으로 완료된 트랜잭션의 결과는 영구적으로 반영된다

## 트랜잭션 병행 처리 시 발생 문제

- 갱신 내용 손실

    어떤 데이터에 여러 트랜잭션이 수행될 때, 하나를 제외한 갱신들이 누락됨

- 현황 파악 오류

    어떤 데이터 갱신이 끝나지 않은 시점에서 다른 트랜잭션이 해당 데이터를 조회할 경우 오류 발생

- 모순성

    트랜잭션 동시 실행 시 DB는 일관성 없고 모순된 상태로 존재

- 연쇄 복귀

    여러 트랜잭션이 하나의 레코드를 갱신할 때, 한 트랜잭션이 롤백하면 다른 트랜잭션도 같이 롤백되는 문제

## 로킹 제어 기법

병행처리 시 발생하는 문제를 방지하는 기법

트랜잭션이 DB의 데이터를 조작할 때, 일정 부분을 Lock시키고 트랜잭션 완료 후 Lock을 반납하는 방법

- 공유 로킹

    Lock이 걸린 데이터는 읽기는 가능, 쓰기는 불가능

- 배타 로킹

    Lock이 걸린 데이터는 읽기, 쓰기 둘 다 불가능

### 로킹 제어 기법 범위 trade-off

- 로킹 제어 범위 클 때 → 관리가 쉽지만 트랜잭션의 병행성이 떨어짐
- 로킹 제어 범위 작을 때 → 관리가 어렵고 오버헤드가 증가하지만, 트랜잭션의 병행성이 증가함

### 로킹 제어 기법 문제점

- 로킹에 따른 트랜잭션 직렬화 가능성이 높아진다(트랜잭션 병행 처리 무의미)
- 데드락 발생 가능성이 높아진다

## 데드락

Lock을 걸어둔 두 트랜잭션이 있을 때,

각 트랜잭션들이 Lock을 걸어둔 서로의 데이터를 참조하기 위해 무한정 대기하는 상황

### 데드락 해결 방법

트랜잭션 하나를 롤백시킨 뒤, 나머지 트랜잭션을 먼저 완료시키고 롤백한 트랜잭션을 순차적으로 작업 재개시키는 작업 직렬화

### 데드락 예방 방법

- 데드락 탐지

    매 트랜잭션 마다 데드락 검사 → 코스트 부담

- 데드락 회피

    시분할 처리를 이용하여 트랜잭션 순차 처리 제공

- write 보다 read가 많은 경우
    1. read용 DB를 slave로 두어 읽기 요청을 전담시킴
    2. write 수행은 master가 처리하며 DB 동기화 수행

**타임 스탬프 기법**

트랜잭션의 식별자로 타임스탬프 지정한다

→ 트랜잭션이 대기하지 않으나 높은 확률로 롤백 발생 및 연쇄 복귀 초래

## COMMIT & ROLLBACK

- commit

    해당 트랜잭션이 반영된 DB 변경사항을 저장하는 것

- rollback

    해당 트랜잭션이 반영된 DB 변경사항을 취소하는 것

# 정규화

어떤 릴레이션의 이상 문제를 해결하기 위해, 속성들의 종속 관계를 분석하여 여러 릴레이션으로 분해하는 과정

→ 분해하면 속도가 상대적으로 느려질 수 있지만, 분해하지 않으면 이상 문제가 발생

## 이상 문제

- 삽입 이상

    데이터 저장 시 원하지 않는 정보가 함께 삽입되는 경우

- 삭제 이상

    튜플 삭제 시 유지되어야 하는 정보까지 연쇄적으로 삭제되는 경우(cascading)

- 갱신 이상

    중복 튜플 중 일부 속성 갱신 시 정보의 모순성이 발생하는 경우

### 함수적 종속?

어떤 속성(필드)이 다른 속성의 값에 따라 결정될 때, 함수적으로 종속되어 있다고 한다

- 부분 함수

    어떤 함수에서 일부분을 담당하는 함수 요소

    e.g., `function(학번, 과목코드)=과목점수`에서 `학번`과 `과목코드`는 각각 부분 함수

- 이행 함수

    이행 규칙을 성립시키는 함수

    **이행 규칙**

    `X→Y` 이고 `Y→Z` 이면, `X→Z` 이다

    e.g., `function(학번)=등록금`에서 `학번` → `과`, `과` → `등록금` 일 때, `학번` → `등록금` (이행규칙 성립)

### 완전 함수적 종속

속성 집합 X에 대해 Y가 함수적으로 종속 될 때, X의 부분집합에 대해서는 Y가 함수적으로 종속되지 않을 경우

## 정규화 단계

- 제 1 정규화: 각 필드 값이 원자값이 되도록 바꾼다
- 제 2 정규화: 각 필드에서 부분 함수 종속을 제거
- 제 3 정규화: 기본키를 제외한 필드 간의 이행 함수 종속을 제거
- 제 BCNF화: 결정자이면서 후보키가 아닌 필드 제거
- 제 4 정규화: 다치 종속성 제거
- 제 5 정규화: 조인 종속성 제거

## 역 정규화 이유

정규화로 테이블이 많이 나눠진 경우 데이터 호출을 위한 JOIN의 비용을 감소시키기 위해 역 정규화

# 데이터베이스 장애

- 트랜잭션 장애

    트랜잭션이 정상적으로 수행되지 못한 장애

- 시스템 장애

    하드웨어, 소프트웨어 고장으로 인한 장애

- 디스크 장애

    디스크 스토리지 일부 및 전체 붕괴로 인한 장애

## 데이터베이스 장애 회복 기법

### 로그 기반 회복 기법

로그를 기반으로 장애 복구

- 지연 갱신 회복 기법

    트랜잭션의 부분 완료 상태까지 이르는 모든 변경 내용을 로그에 저장
    → DB에는 commit 발생 전까지 저장을 지연시키는 방법

    1. 디스크 write 연산을 지연시키고 로그에 DB 변경 내역을 로그에 기록
    2. 트랜잭션 완료 시 로그를 기반으로 지연된 디스크 write 연산 수행
    - 트랜잭션 완료 후 장애 발생한다면 → 회복 시 REDO 연산 실행
    - 트랜잭션 완료 전 장애 발생한다면 → 회복 시 로그 무시(로그 폐기)
- 즉시 갱신 회복 기법

    트랜잭션 수행 시 발생하는 모든 데이터 변경 정보를 로그에 저장

    → DB에는 즉시 모든 변경 사항을 반영하는 기법

    1. 트랜잭션 과정에서 데이터 변경 내역을 로그와 DB에 모두 반영
    - 장애 발생한다면 → 회복 시 트랜잭션 실행 이전의 상태로 복구

        로그 파일을 참조하면서 미완료된 변경에 대해 UNDO 우선 실행

        완료된 변경에 대해서는 REDO 실행

### 체크포인트 회복 기법

일정 기간 단위로 체크포인트 생성하여 장애 복구

장애 발생 시 체크포인트까지 UNDO 실행 후 다시 REDO 실행

### 그림자 페이징 회복 기법

하드디스크에 그림자 페이지를 만들어 장애 복구

장애 발생 시 하드디스크 그림자 페이지로 주메모리 페이지 변경(백업)

장애 미 발생 시 그림자 페이지 테이블 삭제

# 관계형 DB vs 비관계형 DB

### 관계형 DB

데이터 간의 종속성을 관계로 표현하는 DB

데이터는 레코드 단위로 테이블에 저장되고, 이런 테이블은 key-value 관계를 나타낸다

### 비관계형 DB

행과 열로 나타내는 테이블 형식 스키마를 사용하지 않는 DB 

저장되는 데이터 형식의 특정 요구 사항에 맞게 저장소 모델을 사용한다

### NoSQL

SQL문이 아니라 다른 프로그래밍 언어 및 구문을 사용하는 것 (비관계형 DB를 나타냄)

## NoSQL의 장점

- JOIN 처리가 없음 → 노드 확장의 용이성 제공
- 가변적 데이터 구조로 데이터 저장 가능 → 유연성 높음

### NoSQL 단점

- 다양하고 복잡한 쿼리 불가능
- 일관성 절대 보장 X

### NoSQL 사용시기

비정형 데이터를 저장할 때 사용 (정형화된 데이터를 저장할 때는 체계적인 RDBMS가 유리)

