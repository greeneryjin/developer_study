
예외 

: 시스템 중지 없이 지속적인 서비스를 위한 처리 기술 

- error
    - error는 모두 Unchecked Type으로 컴파일 시점에 알 수 없고 런타임에서 발생합니다.
    - 코드로 핸들링 할 수 없는 심각한 오류입니다.
- Exception
    - Checked Type, Unchecked Type으로 나뉘며 코드로 핸들링할 수 있는 오류입니다.

개발자 코드 예외

**Checked Exception**

- 컴파일 시점에 확인할 수 있는 예외를 의미합니다.
- 스프링과 함께 사용할 때 어노테이션 안에서 체크 예외 발생 시, 롤백을 지원하지 않습니다.
- 주로 try {} catch문이나 throws 던져서 예외를 처리합니다.
    
      ex) SQLException, FileNotFoundException
    

**UnChecked Exception**

- 컴파일 시점에 확인할 수 없고 런타임 시점에서 발생한 예외를 의미합니다.
- 스프링과 함께 사용할 때 어노테이션 안에서 체크 예외 발생 시, 롤백을 지원합니다.
- 따로 예외 구문을 처리하는 로직이 없습니다.

       ex) ArrayIndexOutOfBoundException, NullPointerException

예외 처리

```java
try { 
  //예외가 발생할 수 있는 실행문 		 
} catch() {
	//예외 처리문
}
```

e.printStackTrace();
: 클라이언트가 보는 예외가 아니라 서버 실행창에만 출력하는 에러 메세지

<br>

#### 체크 예외 

: 예외를 잡아서 처리하지 않으면 항상 throws에 던지는 예외를 선언해야 합니다.

```java
 /**
 * RuntimeException을 상속받은 예외는 언체크 예외가 된다.
 */
 static class MyUncheckedException extends RuntimeException {
		 public MyUncheckedException(String message) {
			 super(message);
		 }
 }

//체크 예외
static class Repository {
		 public void call() throw MyUncheckedException{
			 throw new MyUncheckedException("ex");
		 }
 }

**static class Service {
	 Repository repository = new Repository();

	 /**
	 * 예외를 잡아서 처리.
	 */
	 public void callCatch() {
		 try {
				repository.call();
  	 } catch (MyUncheckedException e) {
				//예외 처리 로직
				log.info("예외 처리, message={}", e.getMessage(), e);
			  }
     }
		
		 //예외를 잡지않고 밖으로 던짐 
		 public void callThrow() throws MyCheckedException {
			  repository.call();
	   }
}**
```
<br>


#### 언체크 예외

: 언체크 예외는 말 그대로 컴파일러가 예외를 체크하지 않는다는 뜻입니다. 

```java
@Test
void unchecked_catch() {
		 Service service = new Service();
		 service.callCatch();
} 

@Test
void unchecked_throw() {
		Service service = new Service();
		assertThatThrownBy(() -> service.callThrow()).isInstanceOf(MyUncheckedException.class);
}
 
/**
 * RuntimeException을 상속받은 예외는 언체크 예외가 된다.
 */
 static class MyUncheckedException extends RuntimeException {
		 public MyUncheckedException(String message) {
			 super(message);
		 }
 }

 /**
 * UnChecked 예외는
 * 예외를 잡거나, 던지지 않아도 된다.
 * 예외를 잡지 않으면 자동으로 밖으로 던진다.
 */
 static class Service {
		 Repository repository = new Repository();
 
		/**
		* 필요한 경우 예외를 잡아서 처리하면 된다.
	  */
	 public void callCatch() {
		 try {
				 repository.call();
		 } catch (MyUncheckedException e) {
				 //예외 처리 로직
				 log.info("예외 처리, message={}", e.getMessage(), e);
		 }
	 }
   /**
   * 예외를 잡지 않아도 된다. 
   * 자연스럽게 상위로 넘어간다. * 체크 예외와 다르게 throws 예외 선언을 하지 않아도 된다.
   */
   public void callThrow() {
		 repository.call();
   }
 
static class Repository {
		 public void call() { 
				throw new MyUncheckedException("ex");
		 }
 }
```

실무에서는 언체크 예외를 최대한 사용하는 것이 좋습니다.(체크 예외는 잘 사용하지 않음)

서비스 계층을 지나 데이터베이스와 네트워크처럼 시스템(시스템 예외)에서 예외가 발생했다고 가정했을 때, 서비스 계층은 이 둘의 예외를 처리할 방법을 모릅니다. 왜냐하면 서비스 계층을 애플리케이션에 속하지 데이터베이스나 네트워크가 아니기 때문입니다. 

대부분의 예외는 복구가 불가능하고 의존 관계에서 발생하는 예외, 다른 기술(시스템)들을 사용하는 예외들을 개발자가 하나하나 관리하기가 불가능하기 때문입니다. 

그래서 서블릿의 오류 페이지나, 또는 스프링 MVC가 제공하는 ControllerAdvice 에서 이런 예외를 공통으로 처리합니다. 이러한 예외들은 자세하면 보안상의 문제가 발생할 가능성이 크기 때문에  해결이 불가능한 공통 예외는 별도의 오류 로그를 남기고, 개발자가 오류를 빨리 인지할 수 있도록 메일, 알림(문자, 슬랙)등을 통해서 전달해야 합니다. 


개발자가 처리할 수 있는 예외는 체크 예외로 개발자가 처리하고 시스템 예외, 의존 관계에서 발생하는 예외는 언체크 예외로 처리하는 것이 가장 좋습니다. 

<br>

**비즈니스 예외** 

→ 체크 예외를 고려하는 편이 좋습니다. 왜냐하면 시스템이 정상 작동하고 있는 상황에서 잔액 부족과 같은 경우가 발생하여 언체크 예외처럼 롤백하게 되면 고객이 가지고 있는 정보를 전부 버릴 수 있기 때문에 체크 예외로 처리하여 고객에게 발생한 예외 내용을 알려서 비즈니스를 완료할 수 있도록 처리합니다.
