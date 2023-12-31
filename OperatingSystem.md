### ▶️ 운영체제란?

- 사용자가 실행되는 응용 프로그램이 올바르게 실행되도록 돕고, 필요한 자원을 할당해주는 프로그램
- 사용자를 위한 프로그램 (x)
- 사용자가 실행하는 프로그램을 위한 프로그램 (o)
- 현존하는 프로그램 중 가장 큰 프로그램 중 하나
  - ex) 대표적인 운영체제 리눅스 : 코드가 10,000,000줄이 넘어간다고..
  따라서 운영체제가 제공하는 서비스, 기능들이 매우 다양함

**🐵 운영체제의 핵심 기능** :

1. 자원에 접근하고 조작하는 기능
2. 프로그램이 올바르고 안전하게 실행되게 하는 기능

→ 이 두가지를 담당하는 부분을 **커널 kernel** 이라고 한다.

운영체제의 심장, 엔진이라고도 불린다.

따라서 어떤 커널을 사용하냐에 따라 컴퓨터 전체의 성능에 직접적인 영향을 끼친다.

🐵 **커널**

- 일반 서적에서 ‘운영체제’라고 칭하며 설명하는 것의 대부분은 사실 ‘커널’이 하는 일들이다
- 운영체제 기능 중 커널이 하지 않는 기능이 있는데, 대표적으로 **GUI**
  - 우리가 아는 그 기본 구성 화면들.. 아이폰, 안드로이드, 맥북, 윈도우에서 모두 다른 그 UI!
  - 이 친구들은 그저 컴퓨터와 사용자가 상호작용할 수 있도록 운영체제가 지원하는 기능 중 하나일 뿐, 커널과 직접적으로 소통하지 않는다 (앞서 말한 운영체제의 핵심 기능을 보면 알 수 있듯 운영체제의 핵심 기능들과 GUI는 거리가 있다!)

**🐵 운영체제의 핵심 서비스**

1. **프로세스 관리**
   - 프로세스 : 실행 중인 프로그램
   - 작업 관리자의 프로세스 항목에 나와있는 친구들!
   - 일반적으로 CPU는 한 프로세스씩 실행하기 때문에, 한 프로세스를 실행하고 다른 프로세스로 전환하여 실행하기를 반복함 (우리가 다음주차에서 볼 Context Switching과 유관!)
   - 이때, 바로 실행이 가능한 프로세스가 있고, 바로 실행이 불가능한 프로세스가 있을 수 있음 (대표적으로 입출력을 필요로 하는데, 이미 해당 입출력 자원이 사용되고 있는 경우가 있다)
   - 따라서 이러한 부분들을 고려하며 프로세스들의 실행을 관리하는 역할을 운영체제가 담당한다.
2. **자원 접근 및 할당**

   - 모든 프로세스는 실행하기 위해 **자원**을 필요로 한다
   - 각 프로세스는 필요로 하는 자원이 모두 다르다 (당장 우리가 사용하는 프로세스들만 봐도 입출력 기기를 필요로 하는 프로세스가 있고, 없는 프로세스가 있다)

   → 따라서 운영체제가 이렇게 프로세스가 전환됨에 따라 해당 프로세스가 필요로 하는 자원을 그때그때 할당해주고 관리해주는 역할을 하는 것!

   🙋‍♀️**그렇다면 여기서 말하는 자원에는 어떤 것들이 있을까?**

   컴퓨터의 4가지 핵심 자원을 알아보자.

   - **CPU**
     - 컴퓨터 시스템을 통제하고 프로그램의 연산을 실행 · 처리하는 가장 핵심적인 컴퓨터의 제어 장치
     - 앞서 말했듯, CPU엔 하나의 프로세스만 할당이 가능하고 이 역할을 운영체제가 한다고 이야기했다. 결국 그러한 **프로세스 관리**도 `CPU`라는 자원을 관리하는 일종의 **자원 분배** 중 하나!
   - **메모리**
     - 메인 메모리, RAM을 뜻함. 프로그램 실행 시 필요한 주소, 정보들을 저장하고 가져다 사용할 수 있게 만드는 공간.
     - 프로세스가 실행됨에 따라 메모리에 올라올 때, 해당 프로세스가 메모리의 어느 주소에 올라가야 할지 결정
     - 각각의 프로세스는 독립된 메모리 공간, 주소를 갖으며, 한정되어있는 메모리 공간은 효율적으로 사용돼야하기 때문에 운영체제가 이를 관리해준다.
   - **입출력장치**
     - 보조기억장치 및 입출력 장치들이 CPU, 메모리와 어떻게 연결되어있냐에 따라 성능 차이
     - 기존엔 하나의 버스로 연결되어있었지만, CPU와 메모리 성능이 향상되고, 장치도 다양해짐에 따라 입출력을 CPU가 직접 관리하는 것이 비효율적인 등 연결 구조의 개선이 필요했다.
     - 이를 위해 입출력 제어기(I/O Controlloer)가 도입되었고, 입출력 버스가 분리되었다.
     - 이와 관련된 구체적인 내용은 다음 회차에 알아보자 !

3. **파일 시스템 관리**
   - 컴퓨터 사용할 때 수없이 다양한 파일을 생성하고, 조회하고, 삭제한다.
   - 파일들을 묶어 디렉토리로 관리하기도 한다
   - 이러한 파일들을 관리해주는 것도 운영체제의 역할!
