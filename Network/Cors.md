#### CORS

:  브라우저에게 교차 출처를 공유할 수 있는 권한을 부여하도록 브라우저 알려주는 것

   브라우저는 요청을 한 번에 보내지 않고 예비 요청과 본 요청을 나눠 서버에 전달합니다. 
   예비 요청을 보내는 것을 Preflight Request라고 하며 여기서 헤더 정보를 비교하고 
   일치하지 않을 경우에는 CORS가 발생하고 일치할 경우 200 OK를 응답합니다. 

<br>

    출처
    : 프로토콜, 호스트, 포트로 구성된 것 
      

#### CORS 설정 

+ Access-Control-Allow-Origin
  
  : 헤더에 작성된 출처만 브라우저가 리소스를 접근할 수 있도록 허용합니다.
  
+ Access-Control-Allow-Methods
  
  : preflight request 에 대한 응답으로 실제 요청 중에 사용할 수 있는 메서드를 나타냅니다.

+ Access-Control-Allow-Headers
  
  : preflight request 에 대한 응답으로 실제 요청 중에 사용할 수 있는 헤더 필드 이름을 나타냅니다.

+ Access-Control-Allow-Credentials
  
  : 실제 요청에 쿠기나 인증 등의 사용자 자격 증명이 포함될 수 있음을 나타냅니다. Client의 credentials:include 일 경우 true 필수입니다.
   
+ Access-Control-Max-Age
  
  : preflight 요청 결과를 캐시 할 수 있는 시간을 나타내는 것으로 해당 시간동안은 preflight요청을 다시 하지 않게 됩니다.



  
