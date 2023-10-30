# HTTP & HTTPS: 웹 통신의 기초와 보안 버전의 차이

### ▶️ HTTP :

Hypertext Transfer Protocol 

- 클라이언트와 서버 간 통신을 위한 **통신 규칙** 세트 또는 프로토콜
- TCP/IP 위 프로토콜
- for 인터넷 **웹 사이트 로드**
    - HTML, JSON 등 …
- 사용자가 웹 사이트를 방문하면 브라우저가 웹 서버에 HTTP 요청을 전송 → 웹 서버는 HTTP 응답
- `요청` : GET, POST, PUT, DELETE
- `응답` : 1XX, 2XX(성공), 3XX(리다이렉션), 4XX(요청오류), 5XX(서버오류) 상태코드
- **암호화 과정 없이 (평문) 데이터를 주고받기 때문에 서버와 클라이언트의 메시지가 노출될 수 있음**

### ▶️ HTTP**S**

- S : **Over Secure Socket Layer**
- = 보안이 강화된 HTTP
- 만약 사용자의 아이디와 비밀번호를 입력하는 로그인 통신을 HTTP로 하게된다면?
- 이렇게 데이터를 보호해야 할 경우에 **`암호화`를 거치기 위해** 사용하는 프로토콜이 HTTPS

![Untitled-24](https://github.com/do-sopt-cs-study/CS-LydiaCho/assets/81505421/47fe3745-22a0-4c92-9383-10244739749e)

우리에게 익숙한 OSI 7계층은 왼쪽! 

일반적인 **HTTP 통신**의 경우, 클 <> 서 통신 시 최상단인 응용 계층에서 HTTP 프로토콜을 사용한다는 그림이다. 

반면 오른쪽의 그림이 **HTTPS 통신의** 경우인데, 

최상위 응용 계층에서 HTTP프로토콜을 사용하는 것은 동일하지만, 

더 나은 보안성을 위해서 응용계층과 전송 계층 사이에 별도의 보안 계층이 추가로 들어간다. 

이때 보안 계층에서 HTTP의 보안성 증대를 돕는 프로토콜이 앞서 배운 **SSL**인 것!

쉽게 말해, `HTTPS = HTTP + SSL` 라고 할 수 있다.

<img width="506" alt="%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202023-10-28%20%EC%98%A4%EC%A0%84%203 24 49" src="https://github.com/do-sopt-cs-study/CS-LydiaCho/assets/81505421/6152d40d-0f92-425e-94e9-7daacdafc4c0">


이렇게 URL 앞에 https가 표시되어 있다면 ? → 웹사이트가 SSL/TLS 인증서로 보호되는 경우

브라우저창의 **자물쇠 기호**를 클릭해보면 해당 **인증서**를 볼 수 있다.

<img width="604" alt="%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202023-10-28%20%EC%98%A4%EC%A0%84%203 46 38" src="https://github.com/do-sopt-cs-study/CS-LydiaCho/assets/81505421/6f51e651-ff6c-4340-94a8-6beb09758cff">
<img width="604" alt="%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202023-10-28%20%EC%98%A4%EC%A0%84%203 46 52" src="https://github.com/do-sopt-cs-study/CS-LydiaCho/assets/81505421/d38ff19c-f411-487e-8c15-1e5f22019e50">
<img width="604" alt="%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202023-10-28%20%EC%98%A4%EC%A0%84%203 48 58" src="https://github.com/do-sopt-cs-study/CS-LydiaCho/assets/81505421/9d97ce3b-bb8d-4820-b331-cce635fbcfeb">


### 🙋‍♀️ 그런데 딱히 보안이 필요해보이지 않는 사이트도 다 https인데요?

2014년도, Google이 웹 전반의 보안을 개선하고자 모든 **사이트를 대상으로 https 프로토콜**을 사용할 것을 요구.

- 보상 : SSL 보안 사이트에 대해 높은 검색 순위 부여
    - → 따라서 **구글 SEO**(검색 엔진 최적화)**를 위해 https 필요**
- 불이익 : 브라우저에 “안전하지 않음” 표시
