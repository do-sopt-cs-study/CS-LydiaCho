## ▶️ 프로세스

- 프로세스 : **실행중인 프로그램**
- 운영체제(OS)로부터 자원을 할당받는 작업의 단위
  - 여기서 자원은? CPU시간, 주소 공간, (독립된) 메모리 영역 등

🐵 프로세스의 **Context**

- 프로세스가 **현재 어떤 상태**에서 수행되고 있는지 정확히 규명하기 위해 필요한 정보

1. CPU 수행 상태를 나타내는 **하드웨어 문맥**
2. 프로세스의 **주소 공간** : code, data, stack
3. 프로세스 관련 **커널 내의 문맥** : PCB(Process Control Block), Kernel stack (커널 내의 주소)

   > **PCB** : Process Control Block. 운영체제가 프로세스를 관리하기 위해 각 프로세스의 정보를 담아서 관리하는 커널 내의 자료구조.

   <img width="531" alt="R1280x0" src="https://github.com/do-sopt-cs-study/CS-LydiaCho/assets/81505421/477dab68-3561-4a65-8dd0-259395923fa6">


**🐵 프로세스의 상태(state)**

- 프로세스는 상태(state)가 변경되고 수행됨
- **Running**
  - CPU를 잡고 명령어를 수행 중인 상태
  - ex- PC가 레지스터를 잡고 수행 중
- **Ready**
  - CPU를 기다리는 상태 (메모리 등 다른 조건은 모두 만족. CPU만 있으면 당장 수행 가능)
- **Blocked** (wait, sleep)
  - CPU를 줘도 당장 명령을 수행할 수 없는 상태
  - Process가 요청한 이벤트 (ex-I/O)가 즉시 만족될 수 없어서 이를 기다리는 상태
  - ex- 디스크에서 파일을 읽어와야 하는 경우
- **New**
  - 프로세스가 생성 중인 상태
  - ready 상태로 가기 직전 (메모리에 스택 쌓고 등등)
- **Terminated**
  - 수행이 끝난 상태
- **Suspended** (stopped)
  - **외부적인 이유**로 프로세스의 수행이 정지된 상태
  - 프로세스가 통째로 디스크에서 **swap out** 됨 (항상은 아니고 대체로)
    - ex- 사용자가 프로그램을 일시정지 시킨 경우 (ctrl c)
    - ex- 메모리에 너무 많은 프로세스가 올라와있어서 시스템이 프로세스를 잠시 중단시켰을 때
  - **blocked와 suspended의 차이**
    - blocked : 자신이 요청한 event가 만족되면 자동 ready
    - suspended : 외부(OS 등)에서 재시작을 시켜줘야 active

![Untitled-7](https://github.com/do-sopt-cs-study/CS-LydiaCho/assets/81505421/86b8a9f8-68a8-408c-aa6a-a7449899eb34)
![Untitled-8](https://github.com/do-sopt-cs-study/CS-LydiaCho/assets/81505421/17112945-7fed-494d-9284-d529fdb80200)


프로세스 상태도. 중요!

## ▶️ 스레드 (Thread)

- 프로세스 **내**에서 실행되는 여러 흐름의 단위
- 프로세스의 특정한 **수행 경로**
- A thread (or lightweight process) is a basic unit of CPU utilization

🐵 **구성** (독립적인 부분)

- Program Counter
  > 명령을 어디까지 수행했는지를 가리키는 일종의 포인터
- register set
- **stack** space
  > 스레드가 유일하게 독립적으로 가지는 메모리 공간

🐵 동료 스레드와 **공유**하는 부분

- **code** sectioon
- **data** section
- **OS 자원**

🐵 **멀티 스레드**

- 멀티 **스레드**로 구성된 태스크 구조에서는 하나의 스레드가 blocked(waiting) 상태인 동안에도 동일한 태스크 내의 다른 스레드가 실행(running)되어 빠른 처리를 할 수 있음
- **동일한 일**을 수행하는 다중 스레드가 협력하여 높은 처리율(throughput)과 성능 향상을 얻을 수 있음
- 스레드를 사용하면 **병렬성**을 높일 수 있음
  - ex- GPU는 core가 수천개여서, 각 스레드에 뿌려서 동시 진행 시킴
- 결론 : 다중 스레드는 한 프로세스에서 blocked & running이 공존할 수 있다!

![Untitled-9](https://github.com/do-sopt-cs-study/CS-LydiaCho/assets/81505421/082178f5-99e5-49d1-95af-6bbf5e50c5b4)
![Untitled-10](https://github.com/do-sopt-cs-study/CS-LydiaCho/assets/81505421/a6001abb-66f5-4d0a-8bd8-7bcb42ca0fe2)


**🐵 스레드의 장점 (멀티 프로세싱이 아닌, 멀티 스레드를 쓰는 이유)**

- **Responsiveness**
  - ex- 멀티스레드 웹의 경우, 한 스레드(네트워크)가 blocked 되면, 다른 스레드 (display)가 활동
- **자원 효율성 증대**
  - 프로세스 Context Switching 시, CPU register 교체(스레드switching)뿐만 아니라 RAM, 캐쉬 메모리 등등도 모두 초기화해야 함 → 오버헤드 증대
- **Resource** **sharing**
  - N개의 스레드가 code, data, 프로세스 자원을 공유
  - 시스템 자원 소모 감소
  - 통신 부담이 적음
- **Economy**
  - 프로세스간 통신 비용보다 스레드간 통신 비용이 더 적음 (결국 다 자원 공유의 장점과 직결!)
    - 스레드로 Context switching하는 것이, 프로세스 Context Switching(여러 프로세스 갈아끼우기) 하는것보다 비용이 1/5배, 1/30배
  - 프로세스간 전환 속도보다 스레드간 전환 속도가 더 빠름! (stack영역만 처리하면 되니까)

## ▶️ 프로세스와 스레드

- 프로세스는 운영체제로부터 자원을 할당 받는 **작업의 단위**
- 스레드는 **프로세스**가 할당 받은 자원을 사용하는 **실행 흐름의 단위**
  - 프로세스 내에서 진행되는 작업의 갈래

![%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202023-11-12%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%204 42 10](https://github.com/do-sopt-cs-study/CS-LydiaCho/assets/81505421/d91f1226-3dd9-47f3-b66e-931058e890e3)
![%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202023-11-12%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%204 41 56](https://github.com/do-sopt-cs-study/CS-LydiaCho/assets/81505421/81d4dcad-f446-4e69-83de-85af72cb9fc9)


- 각 프로세스당 최소 1개의 스레드(메인 스레드)를 가짐
- 스레드끼리 프로세스의 자원을 공유함
- 프로세스의 4가지 메모리 영역 중 스레드는 Stack만 할당 받아 복사하고,
- Code, Data, Heap은 프로세스 내 다른 스레드들과 공유함
- 즉, 스레드는 각각의 Stack을 가지지만, 나머지는 모두 공유하기 때문에 같은 프로세스 내의 서로 다른 스레드끼리 자원을 함께 읽고 쓸 수 있음
  - 따라서 같은 프로세스 내의 한 스레드가 공유 자원을 변경하면, 이를 다른 스레드가 곧바로 확인 가능
  - 그러나, 프로세스는 각기 다른 주소 공간(자원)을 할당 받기 때문에 다른 프로세스의 변수, 자료구조에 접근 불가능

![%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202023-11-12%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%204 45 31](https://github.com/do-sopt-cs-study/CS-LydiaCho/assets/81505421/880da634-fd89-472a-a929-73e79d5df2a4)


## ▶️ 프로세스의 주소공간

### 🐵 Code

- 프로그래머가 작성한 프로그램 함수들의 코드
- CPU가 해석 가능한 형태로 저장되어있음 (low-level)

### 🐵 Data

- 코드가 실행되면서 사용하는 전역 변수 등 각종 데이터
- 영역 세분화
  - .data : 전역 변수, static 변수 등 프로그램이 사용하는 데이터
  - .BSS : 초기값 없는 전역 변수, static 변수가 저장
  - .rodata : const같은 상수 키워드로 선언된 변수나 문자열 상수

### 🐵 Stack

- 지역 변수와 같이 호출한 함수가 종료되면 돌아와야 하는 임시 자료를 저장
- 함수의 호출과 함께 할당되고, 함수 호출이 완료되면 소멸함
- stack 영역을 초과할 경우 stack overflow 에러 발생

### 🐵 Heap

- 생성자, 인스턴스 같이 동적 할당되는 데이터를 위한 공간
- 사용자에 의해 메모리 공간이 동적으로 할당/해제됨

![%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202023-11-12%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%204 43 40](https://github.com/do-sopt-cs-study/CS-LydiaCho/assets/81505421/80baa5a3-edb1-475c-ae03-81f4e807e735)
