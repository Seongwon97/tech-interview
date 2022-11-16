## Context Switching이란?

CPU는 하나의 프로세스가 독점하는 자원이 아닌 공유를 하는 자원이기에 CPU Scheduling에 따라 실행하는 프로세스가 계속 변경되게 된다. 이때 CPU에서 실행중인 프로세스를 변경하는 것을 Context switching이라고 한다.

- 작업은 OS에서 진행한다.
- context switch는 system call이 아니다. context switch는 OS에서 실행중인 process를 변경해주는 작업이며 system call로인해 context switch가 발생할 수는 있지만 이것이 system call은 아니다.
- process A에서 B로 변경하는 context switch를 하면 A에 PCB에 register값들을 저장해두고 그 후에 B의 PCB에 저장된 register값들을 CPU register에 덮어쓰고 사용을 한다.

## Context Switching Overhead

- context switch를 많이 하면 데이터의 저장 및 불러오는 작업에 의해서 overhead가 발생한다.
- context switch를 줄이면 overhead가 줄어들지만 multi tasking의 timesharing을 하려면 context switch를 할 수 밖에 없어서 이것을 잘 조정해서 해야한다.
