[돌아가기](./README.md)

# 멀티 프로세스

멀티 쓰레드 방식과 다르게, 각각의 분리된 프로세스를 통해서 로직을 수행하는 것

- 프로세스끼리 영향을 끼치지 않음
- 프로세스끼리 완전히 분리된 메모리 영역을 가짐

# 멀티 쓰레드

멀티 프로세스 방식과 다르게, 같은 프로세스 내부에서 동시 다발적으로 다양한 로직을 수행하는 것

- 쓰레드끼리 영향을 끼칠 수 있음
- 쓰레드끼리 공유되는 메모리 영역을 가짐(힙, static / 스택은 쓰레드마다 개인 스택을 가지게 됨)

## 멀티 쓰레드 장점

- 자원 절약

    → 스택을 제외하고, Heap과 같은 메모리 영역을 공유

- 통신의 간편함

    → 전역변수 또는 동적 메모리 할당 영역 Heap을 이용하여 데이터 상호 교환 가능

- 빠른 속도

    → 프로세스 문맥 교환과 달리, 쓰레드 문맥 교환은 캐싱 메모리 제거를 하지 않기에 성능 향상 도모

    시스템의 throughput 향상 + 자원 소모 감소 ⇒ 프로그램의 응답 시간 단축

## 멀티 쓰레드 단점

- 공유 자원에 대한 동기화

    → 쓰레드가 어떤 공유 자원에 접근할 때, 임계영역을 설정하여 상호 배제가 필요

- 과도한 락에 대한 성능 저하

    → 공유 자원이 많을 수록, 락 또한 많아지기 때문에 병목 현상이 발생할 가능성이 생김

## 멀티 프로세스 vs 멀티 쓰레드

### 멀티 프로세스

- 프로세스끼리 영향 x

    → 어떤 프로세스가 예기치 못하게 종료되어도 다른 프로세스는 정상 동작

- 각각의 메모리 및 CPU 할당

    → 자원 낭비 유발

### 멀티 쓰레드

- 쓰레드끼리 영향 o

    → 어떤 쓰레드가 예기치 못하게 종료되면 다른 쓰레드의 동작에 영향을 끼침

- 메모리 공간 절약

    → 프로세스 내부에서 스택을 제외한 모든 메모리 영역을 공유

- 동기화 문제

    → 여러 쓰레드가 같은 데이터나 자원에 동시에 접근하려고 할 때, 상호배제가 요구됨