### Servlet

: 서버 TC/TP 대기, 소켓 연결, HTTP 요청 메세지를 파싱 읽기, POST 방식, Content-Type 확인, HTTP 메시지 바디 내용 피싱, 저장 프로세스 실행, HTTP 응답 메시지 생성, HTTP 시작 라인 생성, Header 생성, 메시지 바디에 HTML 생성에서 입력, 서버 TC/TP 대기, 소켓 연결 종료 등 많은 것들을 서블릿이 전부 처리해줍니다. 

HTTP 요청이 오게 되면 WAS는 Request, Response 객체를 새로 만들어서 서블릿 객체 호출합니다.

### Servlet container

: WAS 서버 내부에 생성되는 공간으로 필요한 서블릿을 보관합니다. 서블릿 객체는 WAS가 생성한 Request, Response 객체를 개발자가 편리하게 사용할 수 있도록 도와줍니다. Request, Response 객체는 요청마다 생성되나 서블릿 객체는 싱글톤으로 공유되어 사용합니다.

Servlet

: .java 파일로 controller 위주로 개발이 권장됩니다. 


JSP

: .jsp 파일로 브라우저에 자바 데이터 출력 용도. 즉 view 위주 개발, 자동으로 servlet으로 변환됩니다. 
