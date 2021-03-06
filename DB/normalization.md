[돌아가기](./README.md)

# 정규화

데이터의 중복을 제거하기 위해 테이블을 분리하는 작업

### 데이터 중복으로 인한 문제

- 데이터 조작 시 이상 현상 발생 가능 (정합성 깨짐 →결함 발생)
- 저장공간 낭비
- 데이터 처리 범위가 넓어져서 조회 성능 하락

# 제 1 정규화

여러개의 속성 값을 갖는 속성의 분리

e.g., 학생 테이블의 자격증 칼럼에 대해

자격증이 여러개 있을 수 있기 때문에, 자격증 속성 분리한다

학생 테이블(with 자격증) ⇒ 학생 테이블 + 학생별 자격증 테이블

# 제 2 정규화

주 식별자 (기본키)에 종속적이지 않은 속성의 분리

(복합 칼럼으로 기본키가 구성되는 경우)

# 제 3 정규화

주 식별자가 아닌 일반 속성에 종속적인 속성 분리

# 역정규화

의도적으로 성능 개선을 위해 데이터 중복시키면서 테이블을 통합하는 작업

### 칼럼 역 정규화

1. 잦은 조인이 일어나는 칼럼 중복 시킴
2. 파생속성(유도 속성)

## 테이블 역정규화

1. 1:1 테이블 통합

    → 두 테이블의 join이 많은 경우

2. 테이블 분할
    - 수직적 분할

        → 칼럼을 분할

    - 수평적 분할

        → 레코드를 분할

3. 요약, 통계 테이블 추가

    e.g., 매출 현황
