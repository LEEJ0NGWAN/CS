[돌아가기](./README.md)

# 데이터 모델링

복잡한 현실세계의 정보를 단순화시켜 표현한 것(가공한 것)

1. 요구사항 수집
2. 요구사항 분석
3. 개념 데이터 모델링

    **모델링의 3대 요소**

    - Entity
    - RelationShip
    - Attribute

    **Entity 설계**

    1. Entity 식별
    2. Entity 간 relationShip
    3. Attribute 식별 (후보키 식별)
    4. 후보키 중 기본키 추출 (나머지 후보키는 대체키)

    3-1. 상세 개념 데이터 모델링(정규화)

4. 논리 데이터 모델링

    개념 모델링 데이터 결과를 "Mapping Rule"에 따라 식별

    - Entity → Table
    - Attribute → Column
    - RelationShip → FK, 또다른 Table (N:M 해소시키기)
5. 물리데이터 모델링

    DB에 구축가능한 형태로 설계

    → 데이터 타입 결정, 제약조건 구체화, 역(반) 정규화
