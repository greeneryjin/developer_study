
### DNS

: 숫자로 된 IP 주소를 사람이 읽을 수 있는 이름으로 변환해서 통신할 수 있도록 작업하는 것

<BR>

### 도메인 주소가 IP로 변환되는 과정

1. 디바이스는 hosts 파일을 열어 봅니다

   + hosts 파일에는 로컬에서 직접 설정한 호스트 이름과 IP 주소를 매핑 하고 있습니다

2. DNS는 캐시를 확인 합니다

   + 기존에 접속했던 사이트의 경우 캐시에 남아 있을 수 있습니다
   + DNS는 브라우저 캐시, 로컬 캐시(OS 캐시), 라우터 캐시, ISP(Internet Service Provider)캐시 순으로 확인 합니다

3. DNS는 Root DNS에 요청을 보냅니다

   + 모든 DNS에는 Root DNS의 주소가 포함 되어 있습니다
   + 이를 통해 Root DNS에게 질의를 보내게 됩니다
   + Root DNS는 도메인 주소의 최상위 계층을 확인하여 TLD(Top Level DNS)의 주소를 반환 합니다

4. DNS는 TLD에 요청을 보냅니다

   + Root DNS로 부터 반환받은 주소를 통해 요청을 보냅니다
   + TLD는 도메인에 권한이 있는 Authoritative DNS의 주소를 반환 합니다

5. DNS는 Authoritative DNS에 요청을 보냅니다

   + 도메인 이름에 대한 IP 주소를 반환 합니다
  

  <br>
  출처: 신입 개발자 전공 지식 & 기술 면접 백과사전
