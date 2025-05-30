### 4.5. CPU코어 수와 스레드 수 사이의 관계는 무엇일까?

CPU 코어 수와 스레드 수 사이에는 어떤 필연 관계도 없다.

### 4.6.2. CPU의 능력 범위: 명령어 집합

- CPU는 다양한 작업을 할 수 있지만, 그 범위는 CPU에 내장된 명령어 집합에 의해 제한된다.

  - 명령어 집합(Instruction Set Architecture, ISA): CPU가 이해하고 실행할 수 있는 명령어들의 집합을 의미함. ADD 명령어처럼 CPU가 수행할 수 있는 기본적인 연산을 정의. 프로그래머가 명령어 집합에 포함된 명령어를 이용해 CPU가 수행할 수 있는 작업도 지정. ( 초기 프로그램은 CPU를 직접 다루는 어셈블리 언어로 작성됨 )
  - 명령어 집합의 중요성
    1. 명령어 집합은 CPU의 핵심 기능을 결정하며, CPU가 할 수 있는 작업을 정의.
    2. 이 명령어 집합에 대한 이해는 CPU를 효율적으로 사용할 수 있는 기초가 됨.

### 4.7. CPU 진화론(중): 축소 명령어 집합의 탄생

- RISC (Reduced Instruction Set Computer)

1. RISC의 탄생 배경 및 특성

   - 명령어 복잡성을 줄임: 복잡한 명령어 하나 대신, 간단한 명령어 여러 개로 같은 작업을 수행하겠다는 방식임. 각 명령어가 수행하는 연산이 단순하고 빠르기 때문에 파이프라인 처리에 유리함.

2. 컴파일러

   - 복잡한 명령어 집합에서는 마이크로코드 정보를 컴파일러가 인지하지 못함.
     하지만 RISC에서는 마이크로코드 없이 CPU의 세부사항을 컴파일러에 제공하여, 컴파일러가 더 강력한 제어권을 가지게 됨.
     이로써 CPU에 대한 최적화가 가능해짐.

3. LOAD/STORE 구조
   - 복잡한 명령어 집합에서는 하나의 명령어로 메모리 접근과 IF, EX, WB 단계를 모두 수행할 수 있음.
   - RISC에서는 명령어가 기본적으로 레지스터 내 데이터만 처리하고, LOAD/STORE와 같은 전용 명령어만 메모리 접근을 담당함. 예시로, 메모리 주소 A, B에 저장된 두 숫자를 곱하는 작업을 수행하려면, 다음과 같음

- 복잡 명령어 집합 예시 (CISC): 이 명령어 하나로 메모리 접근부터 연산까지 모두 수행할 수 있음.

```
MULT A, B
```

- RISC 예시:
  각각의 연산을 단계별로 나누어 수행하므로, 메모리 접근과 연산을 별도의 명령어로 처리해야 함.

```
  LOAD RA, A
  LOAD RB, B
  PROD RA, RB
  STORE A, RA
```

4. 실행 시간 및 파이프라인

   - 복잡한 명령어 집합에서는 명령어 사이에 차이가 크기 때문에 실행 시간이 고르지 않음,
     이로 인해 파이프라인 방식 활용이 어려움.
   - RISC는 간단한 명령어들을 여러 번 사용해서 작업을 처리하기 때문에, 각 명령어가 단순하고 실행 시간이 거의 동일해져서 파이프라인 기술을 도입하기에 적합함.

5. 요약
   RISC는 단순하고 빠른 명령어를 여러 번 사용하여 효율적인 파이프라인 처리를 가능하게 하고, 컴파일러가 CPU의 세부사항을 더 잘 최적화할 수 있도록 설계된 아키텍처.이로 인해 고속 처리와 효율적인 하드웨어 자원 사용이 가능해짐.

### 4.8.3. 하이퍼스레딩이라는 필살기

- 하이퍼스레딩

  - 하나의 CPU 코어에서 두 개의 스레드를 동시에 실행할 수 있게 해주는 기술. 이를 통해 CPU의 성능을 보다 효율적으로 활용할 수 있음.
  - 기존 CPU는 각 CPU 코어가 한 번에 하나의 명령어를 처리했으나, 하이퍼스레딩 기술을 적용하면, 하나의 코어가 두 개의 스레드를 동시에 실행할 수 있게 됨. 즉, 하나의 코어에서 두 개의 스레드가 병렬적으로 작업을 수행할 수 있음.

- 기본 원리

  - 파이프라인이 항상 완벽하게 채워지지 않는 상황에서, 하이퍼스레딩은 빈 공간을 채우기 위해 두 개의 스레드를 동시에 실행함. 이로써 CPU 리소스를 최대로 활용.

- 하드웨어와 소프트웨어 스레드

  - 하드웨어 스레드는 CPU 리소스를 최적화하여 여러 작업을 동시에 처리하도록 지원.
  - 소프트웨어적으로는 각 프로그램이 인식할 수 있는 스레드를 관리하여 성능을 높임.

- 하이퍼스레딩과 운영체제의 관계
  - 하이퍼스레딩은 CPU 하드웨어 기술로, CPU 성능을 높이기 위해 두 개의 스레드를 동시에 처리하는 방식.
  - 운영체제는 하드웨어 자원을 효율적으로 관리하고, 이 기술이 운영체제의 멀티태스킹 관리에 도움을 주는 방식.
  - 따라서 하이퍼스레딩은 CPU 차원의 최적화이지만, 운영체제가 이를 제어하거나 구현하는 것은 아니므로 운영체제와는 직접적인 관계가 없다고 할 수 있다!

### 4.9.1. 레지스터

1. 레지스터와 Context

- 레지스터는 CPU 속도가 매우 빠르지만, 비용이 비싸고 용량에 한계가 있음.
- 프로그램 실행 시 필요한 정보를 메모리에 저장하고, CPU가 사용할 때만 레지스터에 임시로 데이터를 보관함.
- 상황 정보(Context)는 레지스터에 저장된 정보로, 프로그램 실행을 일시 정지하고 재개할 수 있게 해줌.

2. 주요 레지스터와 Context

- 스택 포인터: 스택 프레임이 쌓이는 런타임 스택의 상단 주소 저장.
- 프로그램 카운터(PC): 현재 실행할 명령어 주소 저장.
- 상태 레지스터: 산술 연산에서 발생한 carry나 오버플로우 등 정보를 저장.

3. Context 저장과 복원

- 프로그램 실행 시, 아래 네 가지 상황에서 CPU의 순차적 흐름에서 벗어나게 되며, 이 때 context 저장 및 복원이 필요함.

  - 1. 함수 실행
       : 함수 호출 시, 스택 프레임에 반환 주소 및 레지스터 정보를 저장함. 함수 실행 후 context를 복원하여 이전 함수로 돌아감.

  - 2. 시스템 콜
       : 유저 모드에서 커널 모드로 전환 시, 커널 스택에 유저 프로그램의 레지스터 정보 저장. 시스템 콜 처리 후 context 복원하여 유저 모드로 복귀함.

  - 3. 인터럽트 처리
       : 인터럽트 발생 시, 유저 모드에서 커널 모드로 전환하고, 커널 스택에 context 저장. 인터럽트 처리 후 context 복원하여 유저 프로그램이 재개됨.

  - 4. 스레드 전환
       : 타이머 인터럽트 발생 시, 스레드의 context를 커널 스택에 저장하고, 새로운 스레드의 context를 복원하여 스레드 전환을 수행함.

4. Context 관리
   스택(Stack)은 context 저장과 복원을 위한 중첩 구조에 적합함. 각각의 상황(함수 실행, 시스템 콜, 인터럽트, 스레드 전환)에서는 context를 저장하고 복원하여 실행 흐름을 유지함.
