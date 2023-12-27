
### Cookie

:  클라이언트(브라우저) 로컬에 key-value 쌍으로 저장되는 데이터 파일로 웹서버가 브라우저에 저장하는 데이터입니다. 


#### 사용 목적

(1) 세션 관리 - 로그인 유지, 장바구니, 접속 시간 등을 알 수 있습니다.
(2) 개인화 - 사용자마다 다르게 화면 페이지를 보여줄 수 있습니다.
(3) 트래킹 - 사용자의 행동과 패턴을 분석하고 기록할 수 있습니다.

<br>

### Session

: 일정 시간동안 같은 사용자로부터 들어오는 일련의 요구를 하나의 상태로 보고, 그 상태를 유지시키는 기술

----

### 쿠키와 세션이 필요한 이유 

: HTTP는 Conectionless와 Stateless 특징을 가지고 있습니다. 요청을 끝나면 연결을 끊고 가지고 있던 모든 상태를 없애버리기 때문에 정보가 저장되지 않습니다. 이를 보완하기 위해 쿠키와 세션을 사용하게 되었습니다.


#### 쿠키 & 세션 flow

1. client 로그인: client -> 웹 서버 
2. 최초 접속 시 DB 조회 및 확인: 웹서버 -> DB
3. 회원 정보 기반 세션 생성: 웹서버 -> 세션 저장소
4. Session ID 발급: 세선 저장소 -> 웹서버
5. client 응답 및 쿠키 정보 브라우저에 저장: 웹 서버 -> client
6. client 데이터 요청 + 쿠키: client -> 웹 서버
7. 웹서버에서 응답 후 전달: 웹서버 -> client

세션 생성

```java
      HttpSession session = request.getSession(); 
			System.out.println(session.getId()); 
			//세션 객체에 데이터 저장
			session.setAttribute("name", "연아");
			session.setAttribute("age", 10);
```

쿠키 생성

			//쿠키 객체 생성
			Cookie name = new Cookie("name", "재석");
			Cookie age = new Cookie("age", "40");
			
			//client 시스템에 잔존 시간 설정(1년, 60*60*24*365)
			name.setMaxAge(60*60*24*365);
			age.setMaxAge(60*60*24);
			
			//client 시스템에 몰래 저장(응답객체 통해서 저장)
			response.addCookie(name);
			response.addCookie(age);
