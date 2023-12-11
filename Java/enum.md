
#### Enum

: 상수들의 집합으로 final을 선언해서 기본 자료형의 값을 변하지 않도록 만든 수입니다.

선언 종류

   1. 상수값으로 선언

          public static final int RED = 1;
   
   2. 열거형 클래스 선언 

          enum Color {
            RED.....
          }

  출력 

    Color[] colors = color.values();

장점

: 자동 완성, 오타 검증, 리팩토링, 허용 가능한 값으로 제한 가능 


    
