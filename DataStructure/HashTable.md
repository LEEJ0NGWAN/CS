[돌아가기](./README.md)
# 해시 테이블(Hash Table)

연관 배열 구조를 이용한 key-value 저장 자료구조

### 연관 배열(associative array)

key와 value가 1:1로 연관되어 있는 자료구조

→ key를 통한 value 조회 가능 (통상적인 인덱스의 역할)

### 연관 배열의 기능 종류

- 어떤 key와 value 저장
- 어떤 key의 value 조회
- 어떤 key의 value 변경
- 어떤 key의 value 제거

# 해시 테이블 구성 요소

### 키(key)

해시 테이블에 데이터를 저장시키기 위한 고유 값으로, 해시 함수의 input이 된다

### 해시 함수(hash function)

키를 해시로 변환시키는 역할을 수행하는 함수로, 해시 테이블에 데이터가 효율적으로 저장되도록 한다

- **해시 충돌(Hash Collision)**

    서로 다른 키가 해시 함수를 통해 같은 해시로 변환되어 충돌되는 경우

    → 해시 함수는 해시 충돌을 최대한 줄이도록 만들어야 한다!!

### 해시(hash)

키가 해시 함수를 통해 변환된 결과물로, 해시 테이블에 저장될 값을 가리키는 인덱스 역할을 수행한다

### 값(value)

해시 테이블의 저장소에 저장되는 데이터로 키와 매칭된다

### 저장소(bucket, slot)

값들을 저장하는 보관소로 해시와 매칭된다

# 해시 테이블 기능

### 저장(insert)

새로운 데이터를 저장한다

- 동작

    새로 저장할 데이터와 대응되는 키를 해시 함수를 통해 해시로 변경

    해시를 연관 배열의 인덱스(키)로 사용하여 저장소에 값 입력

- 시간 복잡도

    O(1)

    단, 해시 충돌이 계속 일어나는 최악의 경우 → O(n)

    (모든 버킷의 value를 순회하는 경우)

### 삭제(delete)

어떤 키에 해당되는 데이터를 제거한다

- 동작

    주어진 키를 변환한 해시에 해당되는 값을 찾아 삭제

- 시간 복잡도

    O(1)

### 검색(search)

어떤 키에 해당되는 데이터를 조회한다

- 동작

    주어진 키를 변환한 해시에 해당되는 값을 조회

- 시간 복잡도

    O(1)

# 해시 충돌(Hash Collision)

키를 해시로 변환하는 과정에서, 서로 다른 키가 동일한 해시로 변경되며 겹치게 되는 것

해시 충돌은 필연적으로 발생할 수 밖에 없으나, 최대한 해시 충돌을 피하는 것을 목표로 해야한다

# 해시 충돌 피하기

### 분리 연쇄(Separate Chaining)

해시 충돌이 일어나는 값들을 링크드 리스트 자료구조로 연결해주는 기법

**장단점**

- 장점
    1. 한정된 버킷을 효율적으로 운영 가능
    2. 해시 함수 중요성 및 의존성이 낮아짐
    3. 메모리 절약 가능(저장되는 데이터들에 대한 공간 할당만 요구 됨)
- 단점
    1. 어떤 해시에 데이터가 누적될수록 편향으로 인한 효율성이 낮아진다
    2. 외부 저장 공간을 요구함

**시간 복잡도**

버킷의 수 = n, 키의 수 = m 이라고 가정할 때

O(m/n)

단, 한 버킷에 모든 데이터가 편향될 경우 → O(n)

### 열린 주소 할당(Open Addressing)

해시가 중복될 경우, 비어 있는 해시를 찾아 저장하는 기법

**비어 있는 해시 찾는 규칙**

- 선형 탐색(Linear Probing)

    충돌 해시의 다음 해시(+1) 또는 임의로 건너뛴 해시(+n)에 데이터 저장

- 제곱 탐색(Quadratic Probing)

    충돌 해시의 제곱 해시에 데이터 저장

- 이중 해시(Double Hashing)

    다른 해시 함수를 한번 더 적용한 해시에 데이터 저장

**장단점**

- 장점

    별도의 추가 저장공간 필요 x

- 단점

    해시 함수의 중요성 및 의존성이 높아짐

    데이터 수와 비례하여 필요 버킷 증가

**시간 복잡도**

버킷의 수 = n, 키의 수 = m 이라고 가정할 때

O(1) ~ O(n)

비어 있는 해시를 찾는 횟수에 따라 시간이 달라짐

# 해시 테이블 단점

- 순서가 없기 때문에 순서가 의미가 있는 데이터 저장에 부적절
- 공간 효율성이 낮음

    → 버킷을 사전에 확보하는 것 대비 낭비가 있을 수 있음

- 해시 함수에 대한 높은 의존도
