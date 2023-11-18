### 트랜잭션

: 데이터베이스의 상태를 변화시키기 위해 수행하는 작업 단위(상태를 변화시킨다는 것 → SQL 질의어를 통해 DB에 접근하는 것)

----

### 트랜잭션 성질

* 원자성: 트랜잭션의 연산은 모두 DB에 반영되던지, 전혀 반영되지 않도록 해야함
* 일관성: 트랜잭션의 작업 처리 결과는 항상 일관성 있어야 함
* 격리성: 둘 이상의 트랜잭션이 동시에 병행 실행되고 있을 때, 어떤 트랜잭션도 다른 트랜잭션 연산에 끼어들 수 없음
* 지속성: 트랜잭션이 성공적으로 완료되었으면, 결과는 영구적으로 반영되어야 함

----

### 트랜잭션 특징

: 데이터베이스 시스템에서 병행 제어 및 회복 작업 시 처리되는 작업의 논리적 단위

Commit

하나의 트랜잭션이 성공적으로 끝났고, DB가 일관성있는 상태일 때 이를 알려주기 위해 사용하는 연산

Rollback

하나의 트랜잭션 처리가 비정상적으로 종료되어 트랜잭션 원자성이 깨진 경우

---- 

### DB 병행

: 여러 트랜잭션 사이를 매우 빠르게 이동하면서 처리를 조금씩 수행하는 방식
 

 ### DB 병행 제어(Concurrency Control)
 
: 트랜잭션이 병행 수행될 때 트랜잭션이 데이터베이스의 일관성을 파괴하지 않고, 다른 트랜잭션에 영향을 주지 않도록 트랜잭션 간의 상호작용을 제어하는 것


병행 제어가 없을 경우 발생하는 문제점

1. 갱신 손실(Lost Update)
    
    : 2개 이상의 트랜잭션이 같은 데이터를 공유하여 갱신할 때 갱신 결과의 일부가 없어지는 현상 
    
2. 모순성
    
    :  복수의 사용자가 동시에 같은 데이터를 갱신할 때 데이터들이 상호 일치하지 않아 모순된 결과가 발생
    
3. 연쇄 복귀(Cascding Rollback)
    
    : 병행수행되던 트랜잭션들 중 어느 하나에 문제가 생겨 Rollback되는 경우 다른 트랜잭션들도 함께 Rollback 되는 현상
    
4. 비완료 의존성
    
    : 하나의 트랜잭션 수행이 실패한 후 회복되기 전에 다른 트랜잭션이 실패한 갱신 결과를 참조하는 현상

----

### 트랜잭션 격리 수준

: 여러 트랜잭션이 동시에 처리될 때 특정 트랜잭션이 다른 트랜잭션에서 변경하거나 조회하는 데이터를 볼 수 있도록 허용을 결정하는 것


### 트랜잭션 격리 종류(높은 수준으로 나열)

+ SERIALIZABLE
  
  : 여러 트랜잭션을 순차적으로 진행하는 수준으로 동시에 접근 불가, 동시 처리 성능이 떨어지는 단점이 있음
  

+ Repeatble Read

  : 트랜잭션이 시작되기 전에 커밋된 내용에 대해서만 조회할 수 있는 격리 수준


+ Read Committed 

  : 트랜잭션의 변경 내용이 commit 되어야만 다른 트랜잭션에서 조회할 수 있는 현상


+ Read Uncommitted (Dirty Read 발생 가능)

  : 어떤 트랜잭션의 변경 내용이 commit이나 rollback에 상관없이 다른 트랜잭션에서 보여지는 현상


#### 트랜잭션 격리 발생 문제

+ Dirty Read

  : 동시에 진행되고 있는 다른 트랜잭션(아직 커밋하지 않은 상태)에서 변경한 데이터를 현재 진행 중인 트랜잭션에서 읽어 들이는 것 


+ Non-repeatable Reads

  : 하나의 트랜잭션 중 읽어 들였던 특정 row의 값을 같은 트랜잭션 내에서 다시 읽어 들이는데 중간에 변경사항이 생겨 (실제로 COMMIT이 된 변경사항) 결괏값이 다르게 나오는 현상


+ Phantom Reads

  : 트랜잭션 시작 시점 데이터를 읽었을 때 존재하지 않았던 데이터가 다시 같은 조건으로 데이터를 읽어 들였을 때 존재해 (유령처럼) INCONSISTENT 한 결괏값을 반환하는 현상


