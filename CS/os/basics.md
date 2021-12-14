## 운영체제 기초

### 컴퓨터 기초

컴퓨터 시스템을 운영하는 소프트웨어를 운영체제라고함

- 컴퓨터는 정보(Information)를 처리하는 기계

**정보(Information)**

- 정보의 최소 단위: bit(binary digit)
- 정보의 처리: 정보의 상태 변환(0 <-> 1)
- 부울 대수(Boolean Algebra): NOT, AND, OR (트랜지스터로 만듦)
- 논리 게이트: NOT, AND, OR, XOR, NAND, NOR

**컴퓨터**

- 범용성(Univerality)

  - NOT, AND, OR 게이트만으로 모든 계산 가능
  - NAND 게이트만으로 모든 계산 가능

- 계산가능성(Computability)

  - Turing-computable: 튜링 머신으로 계산 가능한 것
  - Halting Problem(정지 문제): 튜링 머신으로 불가능한 것

- 앨런 튜링: 컴퓨터의 할아버지
- 존 폰 노이만: ISA(Instruction Set Architecture)

**폰 노이만**

Stored-Program(내장형 프로그램) 방식을 처음 도입함

![Screen Shot 2021-12-14 at 7 35 01 PM](https://user-images.githubusercontent.com/38246878/145982228-b54b57f0-598f-41f3-976a-7ff6870f6a2d.png)

- 메모리에 프로그램을 저장하는 컴퓨터
- 프로그램이란, 하드웨어에게 수행할 테스크를 하달하는 명령어들의 집합

### 운영체제(Operating System)

- 컴퓨터에서 계속 실행되는 프로그램(주로 커널, kernel이라고 함)
- 응용 소프트웨어에게 시스템 자원을 할당
- 프로세스를 관리하고, 리소스(파일 등), I/O 등을 관리함

> 컴퓨터는 하드웨어, 운영체제, 응용 소프트웨어, 사용자 네 가지 컴포넌트로 나눌 수 있음

![Screen Shot 2021-12-14 at 7 41 24 PM](https://user-images.githubusercontent.com/38246878/145983159-6150c7b8-2d20-49a7-9bde-92e03c783b94.png)

- **Bootstrap**

전원이 연결되지 않았을 때 OS를 메모리에 로딩하는 것

- **Interreupts**

I/O 디바이스와 통신하는 방법
CPU에다가 신호를 보내고 시스템 버스를 통해서 신호를 전송

![Screen Shot 2021-12-14 at 7 47 09 PM](https://user-images.githubusercontent.com/38246878/145983968-c8f3ef96-dc58-4cb0-a992-edb0f6d96074.png)

- **Von Neumann Architecture**

  - 명령 실행 사이클
    메모리에서 명령어를 fetch
    IR(Instruction Register)에 명령어를 저장함

  - 명령어를 decode
    피연산자를 메모리에서 가져올 수도 있음
    결과를 저장

- **Symmetric Multiprocessing(SMP)**
  여러 개의 CPU가 하나의 메모리를 공유

  ![Screen Shot 2021-12-14 at 7 56 14 PM](https://user-images.githubusercontent.com/38246878/145985286-ac55433f-5f7c-46f0-b213-de2f3814ab76.png)

- **Multi-Core**
  하나의 CPU 안에 Core의 갯수를 늘림

  ![Screen Shot 2021-12-14 at 7 57 14 PM](https://user-images.githubusercontent.com/38246878/145985440-c5a2d458-ffaa-4aa6-a7e2-4c837614f406.png)

- **Multiprogramming**
  메모리에 여러 개의 프로그램을 동시에 올림
  CPU 사용 효율을 높이기 위해 여러 개의 프로세서가 동시에 작동

  ![Screen Shot 2021-12-14 at 7 58 34 PM](https://user-images.githubusercontent.com/38246878/145985650-65a57643-8941-4ddd-bf69-bf904884cc3c.png)

- **Multitasking(Multiprocessing)**
  하나의 CPU가 여러 개의 프로세스를 시분할하여 작동하는 것
  사용자는 모든 프로그램이 동시에 동작하는 것 처럼 보임
  <br/>

- **두 가지의 Operation Mode**
  kernel mode가 아니면 직접적으로 하드웨어를 제어할 수 없음

  ![Screen Shot 2021-12-14 at 8 02 19 PM](https://user-images.githubusercontent.com/38246878/145986470-96709dec-e5c1-4622-abed-87b41f2a7034.png)

> 운영체제에서 가장 중요한 개념은 프로세스와 스레드. 멀티프로세싱(multiprocessing)을 하기 위해서 반드시 발생하는 문제가 동기화(synchronize) 문제. 이것을 제대로 하지 못하면 데드락(deadlock) 문제가 발생함
