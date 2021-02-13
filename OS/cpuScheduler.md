[돌아가기](./README.md)

# CPU 스케줄링

단기 스케줄러에서 Ready Queue에 있는 프로세스에 자원을 할당하는 작업

# 비선점형 스케줄링 정책

- FCFS
- SJF
- Priority Scheduling

### 특징

- CPU burst 완료까지 CPU 반환 x
- CPU 반환 시 스케줄링 수행

## FCFS (First Come First Served)

먼저온 프로세스 순서대로 자원을 할당하는 정책

### 문제점

- convoy effect

    소모 시간이 긴 프로세스 먼저 수행하면,  뒤에 대기하는 짧은 소모 시간의 프로세스들의 평균 대기 시간 증가

## SJF (Shortest Job First)

CPU burst 시간이 가장 짧은 프로세스 순서대로 자원을 할당하는 정책

### 문제점

- starvation

    실행시간이 짧은 프로세스만 선정되기 때문에, 상대적으로 실행시간이 긴 프로세스는 영원히 CPU를 할당 X

# 선점형 스케줄링 정책

- SRT (Shortest Remaining Time first)
- Priority Scheduling

### 특징

- 새로운 프로세스가 Ready Queue에 삽입될 때마다 새로운 스케줄링이 실행됨

## SRT (Shortest Remaining Time first)

현재 수행 프로세스의 남은 cpu burst 시간보다 짧은 burst 시간의 프로세스 도착 시 cpu 선점하는 정책

### 문제점

- starvation

    cpu burst 시간이 긴 프로세스는 burst 시간이 짧은 프로세스가 올 때마다 CPU를 영원히 선점 당함

- 새로운 프로세스 삽입마다 스케줄링이 다시 실행되기 때문에, cpu burst 시간 측정 불가

## Priority Scheduling

우선순위가 가장 높은 프로세스에게 CPU를 먼저 할당하는 정책

선점형 스케줄링 방식, 비선점형 스케줄링 방식 둘 다 존재

### 특징

- 우선순위에 따른 선점

    높은 우선순위의 프로세스가 도착 시 CPU 선점

- 우선순위에 따른 비선점

    높은 우선순위의 프로세스가 도착 시 Ready Queue의 Head에 삽입

### 문제점

- starvation

    우선순위가 낮은 프로세스는 영원히 대기할 수 있다

- 무한 봉쇄 (Indefinite blocking)

    block 상태의 프로세스가 CPU를 영원히 기다리는 상태가 발생

### 해결책

- aging

    오래 기다린 프로세스에 대해 압도적인 우선순위 대우를 적용

# Round Robin

현대적인 CPU 스케줄링 정책

### 특징

- 각 프로세스는 동일 크기의 할당 시간(time quantum)을 가짐
- 할당 시간 소모 시, 프로세스는 선점 당하고 Ready Queue 제일 뒤로 이동
- CPU burst 시간이 제각기인 프로세스가 고루 분포되어 있을 경우 유리
- PCB를 통한 context save가 가능한 경우 실현 가능한 정책

### 장점

- 프로세스의 평균 응답 시간이 빠름

    n 개의 프로세스에 대해 q의 할당 시간이 있는 경우, 각 프로세스의 할당 CPU 시간은 `q = 1/n` 이 된다

    → 어떤 프로세스라도 최대 (n-1)*q 만큼의 시간 내에 응답하게 된다

- 프로세스의 CPU burst 시간에 비례하여 프로세스의 CPU 대기 시간이 증가한다

    → cpu burst 시간에 비례하여 프로세스 간의 공정한 스케줄링 가능

### 문제점

- time quantum 의 trade-off 필요

    할당 시간이 커질 수록 FCFS와 같아지는 비효율성이 생기고, 

    작을 수록 잦은 context switch에 따른 오버헤드 발생
