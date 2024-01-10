
1. export -> JAR file -> jar 파일 생성


에러 발생

       no main manifest attribute in
       
원인  

jar파일에서 처음 호출할 Main 메소드를 찾지 못했다는 에러

---

#### maven build로 jar 파일 생성하는 방법으로 해야함 

project -> 오른쪽 버튼 -> Run as -> Maven clean -> Maven install

project -> 오른쪽 버튼 -> Run as -> maven build

---

#### 리눅스 버전에서 80 사용하면 에러가 발생할 수 있습니다.

     java.net.BindException: Permission denied <null>:80

리눅스에서 Tomcat 접속 포트를 80으로 한 뒤에 일반 사용자 계정으로 startup 했을때 발생하는 문제로

리눅스의 경우 1024 이하의 포트는 well-known port(잘 알려진 포트)라고 해서 루트 권한으로만 실행이 가능합니다.

해결 방법

1. root 권한으로 실행  - root 계정으로 실행하는것은 보안정책상 추천하지 않음

2. apache2 연동  - 다중 톰캣 연동 및 로드밸런싱등을 이용할 수 있음

3. iptable을 이용한 포트 포워딩  - 담당자가 바뀔경우 port 추적관리 어려움이 따름

4. 포트번호 변경


#### java 파일의 파일의 인코딩 문제
		
  1. 문제점
				
      UTF-8을 기본 설정으로 개발되는 구조는 맞으나 경우에 따라 인코딩 이슈 발생
			
   2. 해결책
				
      (1). 문제있는 파일을 인코딩 수정을 해 본다
				
      (2). 1번이 불가할 경우 *.java 를 new로 생성


