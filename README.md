# tech-interview
🧑🏻‍💻 면접 준비를 위한 CS 개념 저장소 🧑🏻‍💻

<details>
<summary><strong>⚙️운영체제</strong></summary>

<br>

[**운영체제란?**](./Operation_System/운영체제란.md)
- 운영체제란 무엇일까요?
- 커널이란 무엇일까요?
- 운영체제는 어떤 기능을 하는지 설명해주세요
- 운영체제가 관리하는 5가지 지원에 대해 설명해주세요

[**프로세스와 스레드**](./Operation_System/Process&Thread.md)
- 프로세스와 프로세서의 차이에 대해 설명해주세요.
- 프로세스와 스레드의 차이를 설명해주세요
- 프로세스의 주소 공간에는 어떤 것이 있을까요?
- 프로세스의 Data, Stack, Heap영역에는 각각 어떤 데이터가 저장되는지 설명해주세요
- 프로세스의 상태에는 어떤 것이 있을까요?
- 프로세스의 Running State에서 CPU 자원을 뺐기는 3가지 상황에 대해 설명해주세요
- OS는 프로세스의 정보를 어떻게 관리하며 어떤 데이터들을 저장하고 있는지 설명해주세요 (hint.PCB)
- PCB가 왜 필요할까요?
- 멀티 스레드와 멀티 프로세스의 차이에 대해 설명해주세요
- 멀티 프로세스 대신 멀티 스레드를 사용하는 이유를 설명해주세요.
- 스레드마다 독립적으로 관리하는 공간은 무엇이며 왜 독립적으로 할당할까요?
- 커널 스레드와 유저 스레드의 차이에 대해 설명해주세요

[**Context Switching**](./Operation_System/Context_Switching.md)
- Context Switching에 대해 설명해주세요
- Context Switching Overhead에 대해 설명해주세요

[**IPC**](./Operation_System/IPC.md)
- 프로세스간 통신은 어떻게 할까요?
- IPC에는 어떤 방법들이 있을까요?

[**System Call**](./Operation_System/SystemCall.md)
- System Call이란 무엇일까요?
- System Call과 Function Call의 차이점에 대해 설명해주세요
- 사용자 모드와 커널 모드에 대해 설명해주세요

[**Interrupt**](./Operation_System/Interrupt.md)
- 인터럽트란 무엇일까요?
- 인터럽트는 시그널을 하드웨어적으로 확인할까요? 소프트웨어적으로 할까요?
- 인터럽트 벡터와 인터럽트 서비스 루틴에 대해 설명해주세요
- 인터럽트 실행 과정에 대해 설명해주세요

[**CPU Scheduling**](./Operation_System/CPU%20Scheduling.md)
- CPU 스케줄링이란 무엇일까요?
- 장기, 중기, 단기 스케줄러로 나누는 기준에 대해 설명해주세요
- 선점과 비선점의 차이에 대해 설명해주세요
- CPU Scheduling의 종류에는 무엇이 있을까요?
- FCFS, SJF, SRTF, Priority scheduling, RR 스케줄링은 각각 무엇이며 장단점은 무엇이 있을까요?
- 선점 스케줄링과 비선점 스케줄링에는 각각 어떤 것이 있을까요?
- Starvation은 어떤 스케줄링에서 발생하는 문제일까요?
- Aging이란 무엇일까요?

[**데드락**](./Operation_System/Deadlock.md)
- 데드락이란 무엇일까요?
- 데드락이 발생하는 4가지 조건에 대해 설명해주세요
- 데드락이 발생할 수 있는 자원의 종류에는 무엇이 있을까요?
- 데드락을 예방, 회피, 무시의 차이에 대해 설명해주세요
- Banker’s Algorithm은 예방, 회피, 무시 중 어떤 방법에 속할까요?

[**Synchronize**](./Operation_System/Synchronize.md)
- 경쟁 상태(Race Condition)에 대해 설명해주세요
- 경쟁 상태(Race Condition)는 어떤 상황에서 발생할까요?
- 경쟁 상태(Race Condition)를 해결하는 방법에는 어떤 방법이 있을까요?
- 임계영역(Critical Section)에 대해 설명해주세요
- Critical Section의 필요조건에는 무엇이 있을까요?
- Thread-safe에 대해 설명해주세요. (hint: critical section)
- Semaphore와 Mutex Lock의 차이에 대해 설명해주세요
- Semaphore에서 발생할 수 있는 문제점에 대해 설명해주세요
- Priority Inversion은 무엇일까요?

[**Memory**](./Operation_System/Memory.md)
- 메모리 계층 구조를 설명해주세요
- 가상 주소는 왜 사용할까요?
- 가상 주소를 물리 주소로 할당하는 3가지 방법은 무엇이 있으며 각각의 특징에 대해 설명해주세요.
- MMU에 대해 설명해주세요
- 캐시란 무엇일까요?
- 캐시의 지역성에 대해 설명해주세

[**Memory Allocation (feat. Paging, Segmentation)**](./Operation_System/Memory%20Allocation.md)
- 메모리 연속 할당(Contiguous Memory Allocation)이란 무엇인지와 장단점에 대해 설명해주세요
- Paging에 대해 설명해주세요
- Paging이 필요한 이유(장때)에 대해 설명해주세요
- Segmentation에 대해 설명해주세요
- Paging과 Segmentation의 차이점에 대해 설명해주세요
- 외부 단편화(External Fragmentation)와 내부 단편화(Internal Fragmentation)에 대해 설명해주세요
- TLB에 대해 설명해주세요

[**Virtual Memory, Page Replacement Algorithm**](./Operation_System/Virtual%20Memory,%20Page%20Replacement%20Algorithm.md)
- 가상 메모리에 대해 설명해주세요
- Swapping에 대해 설명해주세요
- Demand Paging에 대해 설명해주세요
- 페이지 교체의 전반적인 순서에 대해 설명해주세요
- 페이지 교체 알고리즘은 어떤 것이 있을까요?
- LRU 페이지 교체 알고리즘에서 가장 오랫동안 사용하지 않은 Victim Page를 선정하는 방법은 어떤 방법이 있을까요?
- Reference Bit에 대해 설명해주세요

</details>

### [🌿 Spring & JPA](Spring_Q&A.md)
