# HTTP & HTTPS: 웹 통신의 기초와 보안 버전의 차이

- HTTP : Hypertext Transfer Protocol
  - = HTML을 전송하기 위한 통신 규약
  - 암호화 과정 없이 데이터를 주고받기 때문에 서버와 클라이언트의 메시지가 노출될 수 있음
- HTTP**S**
  - S : **Over** Secure Socket Layer
  - = 보안이 강화된 HTTP
  - 만약 사용자의 아이디와 비밀번호를 입력하는 로그인 통신을 HTTP로 하게된다면?
  - 이렇게 데이터를 보호해야 할 경우에 사용하는 프로토콜이 HTTPS

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1d40a623-da7d-44e1-9004-b5b5a8861918/cbc312e4-dbc6-4625-887f-c8baba1ae750/Untitled.png)

우리에게 익숙한 OSI 7계층은 왼쪽이다.

일반적인 **HTTP**의 경우, 클 <> 서 통신 시 최상단인 응용 계층에서 HTTP 프로토콜을 사용한다는 그림이다.

반면 오른쪽의 그림이 **HTTPS**를 사용는 경우인데,

최상위 응용 계층에서 HTTP프로토콜을 사용하는 것은 동일하지만,

더 나은 보안성을 위해서 응용계층과 전송 계층 사이에 별도의 보안 계층이 추가로 들어간다.

이때 보안 계층에서 HTTP의 보안성 증대를 돕는 프로토콜이 앞서 배운 **SSL**인 것!

쉽게 말해, `HTTPS = HTTP + SSL` 라고 할 수 있다.

![스크린샷 2023-10-28 오전 3.24.49.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/1d40a623-da7d-44e1-9004-b5b5a8861918/c4202007-95e1-4a4f-b5f4-f12650e0a007/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2023-10-28_%EC%98%A4%EC%A0%84_3.24.49.png)

이렇게 URL 앞에 https가 표시되어 있다면 ? → 웹사이트가 SSL/TLS 인증서로 보호되는 경우

브라우저창의 **자물쇠 기호**를 클릭해보면 해당 **인증서**를 볼 수 있다.

![스크린샷 2023-10-28 오전 3.46.38.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/1d40a623-da7d-44e1-9004-b5b5a8861918/ad26a87b-1c98-48a7-ade2-d92727d600c9/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2023-10-28_%EC%98%A4%EC%A0%84_3.46.38.png)

![스크린샷 2023-10-28 오전 3.46.52.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/1d40a623-da7d-44e1-9004-b5b5a8861918/3aa94f55-b721-4405-81e9-5b31ce779db7/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2023-10-28_%EC%98%A4%EC%A0%84_3.46.52.png)

![스크린샷 2023-10-28 오전 3.48.58.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/1d40a623-da7d-44e1-9004-b5b5a8861918/bfca91bb-aa9e-4f44-8d1e-4adff27dd69b/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2023-10-28_%EC%98%A4%EC%A0%84_3.48.58.png)

### 🙋‍♀️ 그런데 딱히 보안이 필요해보이지 않는 사이트도 다 https인데요?

2014년도, Google이 웹 전반의 보안을 개선하고자 모든 **사이트를 대상으로 https 프로토콜**을 사용할 것을 요구.

- 보상 : SSL 보안 사이트에 대해 높은 검색 순위 부여
  - → 따라서 **구글 SEO**(검색 엔진 최적화)**를 위해 https 필요**
- 불이익 : 브라우저에 “안전하지 않음” 표시
