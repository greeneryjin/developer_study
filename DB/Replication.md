
#### Replication

: DB를 복제하여 Master 1개와 N개의 Slave 형태로 구성하고 DB간 데이터는 비동기로 동기화해서 데이터를 저장하는 방식

- 장점
    - DB 스케일아웃 → 성능향상
    - 데이터 백업 가능
    - 데이터 지리적 분산
      
- 단점
    - 비동기로 동기화를 하므로 데이터 일관성이 깨질 수 있음 -> Replication lac, Replication 지연
 

  Replication lac 해결 방법
  
  1. 밀리세컨드 단위의 지연은 인정하는 방법
  2. 캐시를 이용하는 방법
  3. Replication lac 문제가 치명적이라면 오라클 DB를 사용
