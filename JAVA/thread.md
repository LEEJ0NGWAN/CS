# Concurrent vs Parallel

### Concurrent

어떤 작업(Job)을 여러개 동시에 처리한다는 개념

e.g., 브라우저 또는 엑셀의 멀티탭

### Parallel

어떤 작업(Job)이 분할되어 여러개의 부분 작업(Sub-Job)이 되고, 이런 부분작업들은 물리적으로 분리된 구조에서 동시에 처리하여 다시 하나로 합치는 개념 → Divide and Conquer와 유사

e.g., 자동차 조립을 위한 여러 사람의 협업, CPU의 멀티 코어

## 관련 용어

### 프로세스

현재 메모리에 적재되어 실행 중인 프로그램

### 쓰레드

프로세스를 구성하는, 독립적인(주체적인) 세부 실행 단위

### 멀티 프로세스

여러 프로세스 동시 수행

### 멀티 쓰레드

한 프로세스 내부에서 여러 쓰레드 동시 수행

# 쓰레드 생성

Java의 쓰레드 생성 방식은 총 2가지 존재

- Runnable interface 구현 방식
    1. implements Runnable 
    2. public void run() 오버라이딩
    3. Thread 객체 생성 시 생성자의 파라매터로 커스텀 Runnable 객체 주입

    ```java
    class MyRunnable implements Runnable {

    	public void run() {
    		...
    	}
    }

    class ThreadTest {

    	public static void main(String[] args) {

    		Thread thread = new Thread(new MyRunnable());
    		thread.start();
    	}
    }
    ```

- Thread class 상속 방식
    1. Thread 상속
    2. public void run() 오버라이딩
    3. 커스텀 쓰레드 생성 및 실행

    ```java
    class MyThread extends Thread {

    	public void run() {
    		...
    	}
    }

    class ThreadTest {

    	public static void main(String[] args) {

    		MyThread thread = new MyThread();
    		thread.start();
    	}
    }
    ```

### main thread

main() 메소드가 실행될 때 동작하는 쓰레드

→ 다른 별도의 쓰레드가 없다면, main thread 하나로 동작(단일 쓰레드)

# JVM과 쓰레드

main() 메소드가 종료되어도, 실행 중인 다른 쓰레드가 있다면 JVM 실행이 종료됨

→ 데몬 쓰레드(GC같이 자바 차원에서 관리하는 쓰레드)를 제외한 응용 쓰레드(사용자가 개발한)의 종료를 확인

### Thread.start() 중복 호출

→ 어떤 Thread 인스턴스가 start() 메소드를 여러번 호출한다면 오류가 발생한다

**Thread는 내부적으로 자신의 상태 관리**

→ 같은 쓰레드 인스턴스에 대해 중복 start 호출 시 쓰레드 내부 상태의 오류로 Exception을 발생시키고 종료됨

# 쓰레드 상태

모든 쓰레드는 `실행` 부터 `종료` 까지 다양한 상태를 가지며 존재하게 된다

→ JVM은 이러한 상태 값들을 이용하여 전체 쓰레드의 실행을 제어

### NEW

새롭게 생성된 쓰레드 인스턴스 상태

→ new Thread().start()

### RUNNABLE

쓰레드가 CPU를 할당받아 작업을 수행할 준비가 된 상태

스레드 스케줄러로부터 자원을 할당 받아 작업을 수행할 준비가 되어 있음

- `WAITING` → `RUNNABLE`

    시간 종료, notify(), interrupt(), I/O 종료 이벤트 발생 시

- `RUNNING` → `RUNNABLE`

    yield() 이벤트 발생 시

### WAITING (+ TIMED_WAITING)

쓰레드가 작업을 수행하다가 일시적으로 대기할 때 할당되는 상태

- `RUNNING` → `WAITING`

    sleep(), wait(), join(), I/O 블로킹과 같은 이벤트 발생 시

### RUNNING

현재 쓰레드가 자신의 작업을 수행 중인 것을 나타내는 상태

### TERMINATE

현재 쓰레드가 자신의 모든 작업을 수행 완료했기 때문에 종료됨을 나타내는 상태

- `RUNNING` → `TERMINATE`

    run() 작업 전부 수행 시

## Thread.sleep()

static method로 호출할 때, ms 단위의 시간을 파라매터로 전달하면 해당 시간만큼 실행 중지 후 재개함

## Thread.join()

Thread 객체는 다른 특정 Thread 객체가 종료될 때까지, 수행하던 자신의 작업을 일시 정지 시킴

→ 그 특정 쓰레드의 작업이 종료된다면, 다시 작업을 재개할 수 있음

## Thread.interrupt()

대기 풀에 존재하는 특정 쓰레드 객체를 방해(interrupt)해서 `WAITING`에서 다시 `RUNNABLE` 상태로 복귀 시킴

```java
thread.start();
...
thread.sleep(50000);
...
thread.interrupt();
```

## Thread.yield()

static 메소드로 지금 당장 Job 수행할 필요가 없는 경우 호출

→ yield 호출 시 다른 RUNNABLE 상태의 쓰레드 객체에게 자원을 양보함

(단, `WAITING` 상태가 아니라 `RUNNABLE` 상태로 이동하기 때문에, 언제든지 경쟁에서 다시 이길 수도 있다)

# synchronized

쓰레드 간의 동기화 작업을 지원하기 위해 사용되는 임계영역 설정 키워드

메소드에 추가 키워드로 붙을 수 있으며, 순수 블록에 사용되어 동기화가 진행될 목표 객체를 설정할 수도 있음

### 메소드 동기화 방식

```java
class Sync {

	public synchronized void foo() {
		...
	}
}
```

### 블록 동기화 방식

```java
class Sync {

	public void foo() {

		synchronized (this) {
			...
		}
	}
}
```

어떤 방식을 사용하던 상관 없이 목표 객체에 대해 mutex lock을 설정해주게 되는데, 

메소드 방식은 해당 메소드를 가지고 있는 클래스를,

블록 방식은 synchronized 뒤에 따라오는 괄호에 파라매터로 입력되는 객체를 mutex lock 대상으로 설정한다

# DeadLock

각 쓰레드들이 서로 다른 공유 자원을 Synchronized로 확보하고 있는 상황에서,

서로가 소유하고 있는 공유자원을 추가 요청하기 때문에 쓰레드가 작업을 진행하지 못하고 영원히 대기하는 상황

→ 주로, 중첩된 synchronized 구조에서 발생

synchronized block을 최대한 작게 구성하는 것이 권장됨

### wait()-notify()-nonifyAll()

- 공유자원.wait()

    현재 작업을 수행할 수 없는 쓰레드가 잠시 lock을 반환하고 대기하다가 추후에 작업을 재개하도록 설정

    → Waiting Pool로 들어가서 대기하고, 후에 Runnable 상태로 바뀌어 Lock을 획득

- 공유자원.notify()

    Waiting Pool에서 한개의 쓰레드에게 어떤 공유 자원이 준비되었음을 알림

- 공유자원.notifyAll()

    Waiting Pool의 모든 쓰레드에게 어떤 공유 자원이 준비되었음을 알림

    ⇒ 통지를 받은 쓰레드 객체들이 경쟁을 하며 기회를 얻음
