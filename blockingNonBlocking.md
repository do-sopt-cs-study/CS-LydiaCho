# Blocking, Non-blocking I/O (비동기, 동시식 I/O의 차이와 활용)

- **Blocking** : 자신의 작업을 진행하다가 다른 작업이 시작되면, 다른 작업이 끝날 때까지 기다렸다가 자신의 작업을 시작하는 것
  - 네트워크 호출, 파일 시스템에서 데이터를 읽고 쓰는 등의 I/O 작업에서 주로 사용됨
  - 단점 : 단일 스레드에서 여러 작업을 처리하는 경우, 다른 작업을 중지시켜야하기 때문에 전반적인 시스템 처리량에 영향을 미칠 수 있음
  <img width="408" alt="%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202023-11-05%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%209 53 19" src="https://github.com/do-sopt-cs-study/CS-LydiaCho/assets/81505421/17795913-3670-43a2-a1ff-138b2368afd5">

- **Non-Blocking** : 다른 작업에 관계 없이 자신의 작업을 하는 것
  - 대규모 서버 애플리케이션, 다중 스레딩 및 이벤트 루프를 사용하는 경우
  - 복잡한 코드 및 에러 핸들링이 필요함
  <img width="502" alt="%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202023-11-05%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%209 54 09" src="https://github.com/do-sopt-cs-study/CS-LydiaCho/assets/81505421/9eab8309-e5d1-4fe9-bb94-f85c2b888a99">


⇒ 다른 주체가 작업할 때 자신의 제어권이 있는지 없는지

### ▶️ Sync & Async

- Synchronous : 작업을 동시에 수행하거나, 동시에 끝나거나, 끝나는 동시에 시작함을 의미
  - Blocking과 달리, A가 B에게 일을 요청한 뒤, A가 아무것도 못하고 B가 일을 마칠 때까지 기다릴 필요는 없음. 하지만 다른 일을 하다가도 B가 요청한 일을 마치면 그 결과에 바로 관심을 가짐
- Asynchronous : 시작, 종료가 일치하지 않고, 끝나는 동시에 시작을 하지 않음을 의미
  - A가 B에게 일을 요청하고, B가 요청한 일을 마쳤어도, 해당 결과를 바로 처리할지 아니면 나중에 처리할지 마음대로 할 수 있음. 즉 B에게 요청한 일의 결과가 A의 다른 작업에 영향을 끼치지 않는 것

⇒ 결과를 돌려주었을 때 순서와 결과를 바로 처리를 해야 하는지 아닌지

⇒ Blocking / Non-Blocking : 제어의 관점

⇒ Sync / Async : 순서와 결과(처리)의 관점

### ▶️ Blocking & Non-blocking X Sync & Async

두가지 분류는 독립적인 개념이기 때문에 각각을 조합하여 사용할 수 있다.

- Blocking & Sync
  - 예시
  ![Untitled-5](https://github.com/do-sopt-cs-study/CS-LydiaCho/assets/81505421/a08e162f-7894-4b2f-b65e-62d81d0bf76f)

  - Scanner로 입력을 받는 동안 제어권이 넘어감 → Blocking
  - 입력받은 결과를 리턴받아서 다음의 작업을 바로 처리 → Sync
- Non-blocking & Sync
  - 예시
  ```jsx
  device = IO.open()
  ready = False
  while not ready:
      print("There is no data to read!") # 다른 작업을 처리할 수 있음

      # while 문 내부의 다른 작업을 다 처리하면 데이터가 도착했는지 확인한다.
      ready = IO.poll(device, IO.INPUT, 5)
  data = device.read()
  print(data)

  # 출처: https://velog.io/@codemcd/Sync-VS-Async-Blocking-VS-Non-Blocking-sak6d01fhx
  ```
  - while 문 안에서 자신의 작업을 처리 → Non-blocking
  - 결과가 리턴됐을 때는 while문을 빠져나가 device에서 값을 읽음 → Sync
- Blocking & Async
  - 결과를 바로 처리하지 않아도 됨에도 불구하고 다른 작업을 못하고 기다려야하는 케이스 (드문 경우)
- Non-Blocking & Async
  - 예시
  ```jsx
  fetch("url", option)
    .then((response) => {
      return response.json();
    })
    .then((data) => {
      doSomething(data);
    });
  ```
  - API 요청을 하고 다른 작업 → Non-blocking
  - 콜백을 통해 추가적인 작업 처리 → Async
