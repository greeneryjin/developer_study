
deptno가 10 아닌 직원들 사번, 부서번호만 검색

        SELECT ename, empno
        from emp 
        WHERE deptno != 10;

        SELECT ename, empno
        from emp 
        WHERE deptno <> 10;

        SELECT ename, empno
        from emp 
        WHERE not deptno = 10;

comm이 300 or 500 or 1400인 값

    -- 비효율적인 계산
    select ename, comm
    from emp e
    WHERE comm = 300 or comm = 500 or comm = 1400

    SELECT ename, COMM
    from emp 
    WHERE comm in (300, 500, 1400);

    
comm이 300 or 500 or 1400이 아닌 사원명 검색

    SELECT ename, COMM
    from emp 
    WHERE not comm in (300, 500, 1400);

comm null인 사원을 asc 정렬 시 검색 -> null부터 나옴, 
                  desc null은 마지막에 나옴
                  
    SELECT ename, COMM
    from emp 
    order by comm asc;

    SELECT ename, COMM
    from emp 
    order by comm desc;


날짜 타입의 범위를 기준으로 검색(BETWEEN), 1980-12-17 ~ 1981-05-01 사이에 입사한 사원명, 입사일 검색

    SELECT hiredate 
    from emp 
    WHERE hiredate BETWEEN '1980-12-17' and '1981-05-01';


지정한 자리수 이하 버리는 함수 : TRUNCATE()

    SELECT TRUNCATE(1234.56789 ,1) FROM DUAL;
    -- 1234.5
 
    SELECT TRUNCATE(1234.56789 ,4) FROM DUAL;
    -- 1234.5678
 
    SELECT TRUNCATE(1234.56789 ,-1) FROM DUAL;
    -- 1230
 
    SELECT TRUNCATE(1234.56789 ,-2) FROM DUAL;
    -- 1200


나누고 난 나머지 값 연산 함수 : mod()

    SELECT MOD(10, 3)

사번(empno)이 홀수인 사원의 이름(ename)

    SELECT ename, empno from emp WHERE MOD(empno, 2);

  
대문자로 변화시키는 함수

    upper() : 대문자[uppercase]
    lower() : 소문자[lowercase]

문자열 일부 추출 함수 : substr()

    SELECT SUBSTR(hiredate, 1, 4) from emp;
    //연도만 나옴

    SELECT hiredate  
    from emp
    WHERE SUBSTR(hiredate, 6, 2) = '02'; 

sysdate() & now(): 날짜 시분 초, curdate() : 날짜    

    SELECT SYSDATE(), NOW(), CURDATE(); 


DATE_SUB() 날짜, 시간 빼기

    SELECT DATE_SUB(NOW(), INTERVAL 1 SECOND)

DATEDIFF() 두 기간 사이의 일수 계산 

    SELECT DATEDTFF('2021-12-31', '2022-02-29);


두 날짜 사이의 개월수 검색 : months_between()
      
    SELECT NOW(), DAYOFYEAR(NOW());  

숫자를 문자로 변환

    SELECT CAST(1 as char(10));

문자를 숫자로 변환

    SELECT CAST('1' as signed) as date1;


날짜로 변형시키는 함수

    select str_to_date('August 10 2023', '%M %d %Y');

*** 조건식 함수 ***

    decode()-if or switch문과 같은 함수 ***
    -- job이 ANALYST 5%인상(sal*1.05), SALESMAN 은 10%(sal*1.1) 인상, 
    -- MANAGER는 15%(sal*1.15), CLERK 20%(sal*1.2) 인상
    
    SELECT ename, sal, job, 
    case job
    	when 'ANALYST' then sal * 1.05
    	when 'SALESMAN' then sal * 1.1
    	when 'MANAGER' then sal * 1.15
    	when 'CLERK' then sal * 1.2
    	else sal
    end as '연봉인상'
    from emp;

Inner JOIN

: 교집합, 공통적인 SELECT 됨

LEFT(OUTER) JOIN

: 조인 기준 왼쪽에 있는 것 전부 다 SELECT

RIGHT(OUTER) JOIN

: 조인 기준 오른쪽에 있는 것 전부 SELECT

OUTER JOIN

: 두 테이블 전부 뽑기


Group by

+ GROUP BY은 WHERE와 ORDER BY 절 사이에 위치합니다.
+ 그룹화할 칼럼은 GROUP BY 절 다음에 넣습니다.
+ SELECT 절에 명시한 칼럼이나 표현식에 별칭을 부여하면 GROUP BY 절에 해당 별칭을 명시해도 데이터가 조회됩니다.
+ 그룹화를 하면 해당 열의 개수가 늘어남

HAVING

+ WHERE 절처럼 조회되는 로우를 걸러내는 필터입니다.
+ 집계함수나 GROUPING() 함수에서만 사용 가능합니다.

 ----- 
  
형 변환 함수

+ CASE

  : 연산자로 흐름 제어 함수입니다.

      CASE value WHEN compare1 THEN result1
      WHEN compare2 THEN result2
      ELSE result
      END;

  -> CASE 다음에 오는 value 값을 WHEN 다음에 있는 compare1 값과 비교하여 두 값이 같으면 result1를 반환합니다.
     아닐 경우, 두 번째 compare2 값과 비교하여 result2를 반환하고 모두 같지 않으면 result를 반환하고 함수가 종료됩니다.

      CASE WHEN compare1 THEN result1
      WHEN compare2 THEN result2
      ELSE result
      END;

      CASE WHEN compare1 THEN result1
      ELSE result
      END;

  -> CASE WHEN 다음 compare1이 참이면 result1을 반환하고 compare2가 참이면 result2를 반환합니다. 그 어떤 조건도 만족하지 않으면 ELSE 다음의 값인 result 반환합니다.


  
     
    






