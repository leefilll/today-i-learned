## 프로세스와 스레드

### 멀티프로그래밍

- 여러 프로세스를 동시에 실행하기 위함
- CPU 사용 효율성 극대화

- **Time Sharing**
  CPU Core를 프로세스 간에 자주 변경해줌
  사용자 입장에서는 각 프로그램이 동시에 실행 되는것 처럼 느껴짐

### 프로세스(Process)

컴퓨터에서 연속적으로 실행되고 있는 컴퓨터 프로그램

- 메모리에 올라와 실행되고 있는 프로그램의 인스턴스(독립적 개체)
- 운영체제에서 시스템 자원을 할당 받는 작업의 단위(독립된 메모리 영역)
- 기본적으로 프로세스는 최소 1개의 스레드(메인)을 가짐
- 각 프로세스는 별도의 주소 공간에서 실행되며, 한 프로세스는 다른 프로세스의 변수나 자료구조에 접근할 수 없음
- 다른 프로세스에 접근하려면 프로세스 간의 통신(IPC, Inter-process communication) 사용
  <br/>
- **프로세스의 상태(process state) 라이프사이클**

  - **New**: 프로세스가 생성됨
  - **Running**: 명령이 실행됨
  - **Waiting**: 프로세스가 이벤트를 기다리는 중(I/O 등)
  - **Ready**: 프로세스가 프로세서에 할당되는 것을 기다리고 있음
  - **Terminated**: 프로세스의 실행이 끝남

  ![Screen Shot 2021-12-14 at 8 23 43 PM](https://user-images.githubusercontent.com/38246878/145989362-96f9af37-2bce-4126-b4da-c5859121c8d2.png)

  - **Scheduling Queue**
    프로세스가 생성되면, CPU Core의 **ready queue**에 들어감
    어떤 I/O나 이벤틀르 기다리는 프로세스는 **wait queue**에 들어감
    주로 linked list로 구현
    ![Screen Shot 2021-12-14 at 8 59 41 PM](https://user-images.githubusercontent.com/38246878/145994373-ba17f1d1-9b66-4423-892f-e131bca39fc3.png)

    <br/>

  > PCB(Process Control Block) 혹은 TCB(Task Control Block) 구조체를 이용하여 프로세스를 관리

- **Context Switch**
  ![Screen Shot 2021-12-14 at 9 12 05 PM](https://user-images.githubusercontent.com/38246878/145996017-9b21b1a3-14a1-4ae7-974b-01eb8575c8c2.png)

  프로세스의 상태를 Context라고 함. interrupt가 발생했을 때, 시스템은 현재 실행되고 있는 프로세스의 context를 PCB 안에 저장하고 나중에 다시 불러서 진행함.
  Context Switch란, CPU core가 현재 진행 중인 프로세스를 다른 프로세스로 전환하는 것. 하나의 상태는 저장하고 다른 하나는 복구시킴.

### 스레드(Thread)

프로세스 내에서 실행되는 여러 흐름의 단위

- 프로세스의 특정한 수행 경로
- 프로세스가 할당받은 자원을 이용하는 실행의 단위
- 스레드는 프로세스에서 메모리 영역의 각각 Stack 부분만 따로 할당 받고, 나머지 영역은 공유
- 같은 프로세스에 속한 다른 스레드와 코드, 데이터 섹션, 파일이나 신호와 같은 운영체제 자원을 공유

**스택을 따로 할당하는 이유**
스택은 함수 호출 시 인자, 되돌아갈 주소값 및 함수 내의 변수 등을 저장하기 위한 공간. 스택 메모리 공간이 독립적이라는 것은 독립적인 함수 호출이 가능하다는 것이고 이는 개별의 실행 흐름이 추가되는 것을 의미. 즉, 독립적인 실행 흐름을 추가하기 위한 최소 조건으로 독립된 스택을 할당하는 것.

> 멀티 프로세싱보다 멀티 스레딩이 더 장점이 많음. Context(Program Counter/PC와 CPU Registers 정보) Switching에서 오버헤드가 발생하기 때문. 단순히 CPU 레지스터 교체 뿐 아니라, 캐시 메모리에 대한 데이터까지 초기화 됨. 또한 멀티 스레드로 실행 시, 프로세스를 생성하여 자원을 할당하는 시스템 콜이 줄어듦.
