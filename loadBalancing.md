# 로드밸런싱 : 서버 부하 분산 기술

- 서버에 네트워크 트래픽을 효율적으로 분산하는 프로세스
- 목적 :
  - 애플리케이션 가용성 최적화
  - 긍정적인 최종 사용자 경험
- 형태 :
  - HW : 온프레미스에 설치하는 물리적 기기
  - SW : 개인 소유 서버에 설치하거나 관리형 클라우드 서비스로 이용
- 역할 :
  - 들어오는 클라의 요청을 실시간으로 중재
  - 어떤 서버가 들어온 요청을 잘 처리할 수 있을지 결정

### ▶️ 알고리즘

#### ✔️ 라운드 로빈
![Round_Robin_Schedule_Example](https://github.com/do-sopt-cs-study/CS-LydiaCho/assets/81505421/3261ef7e-9f85-4435-b1f2-2dc99faa69fc)
![roundrobinmodified](https://github.com/do-sopt-cs-study/CS-LydiaCho/assets/81505421/46fb295d-2369-43a1-b695-dadea800f593)


  - 요청을 순서대로 분배하는 방식
  - 요청이 도착할 떄마다 다음 순서의 서버를 선택하고 요청 전달
  - 모든 서버가 비슷한 수준의 부하를 가질 때, 각 서버의 처리능력이 동일할 때 유용

#### ✔️ 가중 라운드 로빈
![WRR-Examples svg](https://github.com/do-sopt-cs-study/CS-LydiaCho/assets/81505421/b07d8c05-af72-4ee0-abaf-b07718e44a87)
![loadbalancerwightedroundrobin](https://github.com/do-sopt-cs-study/CS-LydiaCho/assets/81505421/40d5113b-0a12-4871-90d2-300516dc8f55)

  - 라운드 로빈의 확장 버전
  - 각 서버나 서비스에 가중치를 부여함 (가중치 더 많은 서버에는 더 많은 요청이 전달)
  - 서버의 처리 능력에 따라 부하 조절하는데에 유용
  - 가중치를 동적으로 조절해서 실시간 부하 분산도 가능
  
#### ✔️ IP 해시
![DTC-source-10](https://github.com/do-sopt-cs-study/CS-LydiaCho/assets/81505421/14688ad4-51df-4b89-896c-b2f83f698c82)

  - 클라이언트 IP 주소를 기반으로 분배
  - IP 주소를 해시 함수에 입력으로 사용해서 서버 선택
  - 동일한 클라 IP 주소로부터 오는 요청은 항상 같은 서버로 라우팅 가능
    - 클라와 서버 간의 상태 유지에 유용, 세션 유지 필요한 앱에 적합

#### ✔️ 최소 연결
![leastconnections](https://github.com/do-sopt-cs-study/CS-LydiaCho/assets/81505421/8e9acf52-0738-49be-a567-ad4116ba1f8e)

  - 각 서버의 현재 연결 상태 모니터 후 연결 수가 가장 적은 서버 선택하여 요청 분배
  - 부하가 서버 간에 균일하게 분산될 수 있음
  - 가장 빠르게 응답하는 서버에게 더 많은 요청이 전달

#### ✔️ 최소 응답 시간
  - 서버의 현재 응잡 능력을 고려, 가장 빠른 응답 시간 가진 서버 선택하여 분배
  - 실제 부하 상황을 고려해서 더 빠르게 응답하는 서버에게 더 많은 요청 보냄
  - 서버간의 부하가 균일하게 분산 가능

### ▶️ 장점

- 가용성
  - 들어온 요청을 서버로 라우팅하기 전에, 서버의 상태를 확인함
  - 어떤 한 서버가 문제가 생기거나 오프라인 상태일 경우, 온라인 상태인 서버에게 로드를 재라우팅
  - → 서비스 중단을 방지하고 고가용성 유지
- 확장성
  - on-demand 고성능 인프라 구현 가능
  - 물리적 서버, 가상 서버 등 추가 및 제거 가능
- 보안
  - SSL 암호화, WAF (방화벽), 멀티팩터 인증(MFA) 등의 보안 기능 포함 가능
  - 보안 개선을 위한 ADC(Application Delivery Controller)에 통합 가능
  - DDoS 공격 등의 보안 위험 방어
