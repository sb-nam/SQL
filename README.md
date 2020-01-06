# SQL

```sql
select Ename,upper(ename),lower(ename),initcap(ename) from emp; -- 대소문자 구분

select * from emp where upper(ename) like upper('%smith%');                                                                       
select * from emp where upper(ename)=upper('smith'); -- 대문자로 이름 변경

select initcap(ename) from emp; -- 앞 글자만 대문자

select ename,length(ename) from emp; -- 이름 출력,(함수) 글자수 출력

select ename,length(ename) from emp where length(ename)>=6;

select length('한글'),length('한글화'),length('english') from dual;
--임시 연산이나 함수의 결과값 확인 용도 dual.

select job,substr(job,1,2),substr(job,3,2),substr(job,5) from emp;

-- 잡의 1번째 부터 2개 출력, 3번째 부터 2개 출력 , 5번째 부터 다 출력.

select job, substr(job, -length(job)), -- 전부 출력.

            substr(job, -length(job),2), -- 앞 2글자 출력.
            
            substr(job,-3) from emp; -- 뒤 3글자 출력 .        

select instr('hello, oracle!','l')as instr_1, --첫번째 만나는 l의 위치   
instr('hello, oracle!','l',5)as instr_2, -- 5번째부터 l의 위치   
instr('hello, oracle!','l',2,2)as instr_3 --2번째부터 2번째 l의 위치    
from dual; -- 임시로 결과 확인 해보겟다.    

select * from emp where instr(ename,'S') > 0;  
select * from emp where ename like '%S%'; -- ename에 S가 있으면 출력   

SELECT '010-1234-5678' AS REPLACE_BEFORE, -- 원본  
REPLACE('010-1234-5678','-',' ') AS REPLACE_1, -- '-'대신 ' ' 출력   
REPLACE('010-1234-5678','-') AS REPLACE_2 -- '-' 제거  
FROM DUAL; -- 임시 결과 확인.

SELECT CONCAT(EMPNO,ENAME),                                                       
-- 두문자를 합치는 CONCAT EMPNOENAME 출력.                            
CONCAT(EMPNO,CONCAT(':',ENAME))    
-- EMPNO:ENAME 출력.                                   
FROM EMP WHERE ENAME = 'SMITH';    
-- ENAME이 스미스 출력.

SELECT EMPNO || ENAME, EMPNO || ':' || ENAME FROM EMP;
-- 문자와 문자 사이를 연결해주는 연산자 ||;

SELECT '[' || TRIM(' _Oracle_ ')||']' AS TRIM,                
--  양쪽의 공백 모두 제거                                                                                       
'[' || TRIM(LEADING FROM ' _Oracle_ ')||']' AS TRIM_LEADING,               
--  왼쪽의 공백 제거                                                                               
'[' || TRIM(TRAILING FROM ' _Oracle_ ')||']' AS TRIM_TRAILING,                 
-- 오른쪽의 공백 제거                                                                     
'[' || TRIM(BOTH FROM ' _Oracle_ ')||']' AS TRIM_BOTH
-- '    ' 안의 공백 제거                                                                     
FROM DUAL;    -- 임시 결과 확인.

SELECT '[' || TRIM('_'FROM'_Oracle_')||']' AS TRIM,                                                                    
'[' || LTRIM('_Oracle_')||']' AS LTRIM,                                                           
'[' || LTRIM('<_Oracle_>','_<')||']' AS LTRIM_2,                                                      
'[' || RTRIM('_Oracle_')||']' AS RTRIM,                                            
'[' || RTRIM('<_Oracle_>','>_')||']' AS RTRIM_2                                       
FROM DUAL;

SELECT ROUND(1234.5678) AS ROUND, -- 소수점 1번째 반올림 후 출력                                        
ROUND(1234.5678,0) AS ROUND_0, -- 소수점 1번째 반올림 후 출력                                       
ROUND(1234.5678,1) AS ROUND_1, -- 소수점 2번째 반올림 후 출력                                
ROUND(1234.5678,2) AS ROUND_2, -- 소수점 3번째 반올림 후 출력                                    
ROUND(1234.5678,-1) AS ROUND_MINUS1, -- 1의 자리를 반올림 후 출력                                
ROUND(1234.5678,-2) AS ROUND_MINUS2 -- 10의 자리를 반올림 후 출력                                  
FROM DUAL;                                               

SELECT TRUNC(1234.5678) AS TRUNC, -- 소수점 1번째 버림 후 출력                                         
TRUNC(1234.5678,0) AS TRUNC_0, -- 소수점 1번째 버림 후 출력                               
TRUNC(1234.5678,1) AS TRUNC_1, -- 소수점 2번째 버림 후 출력                                
TRUNC(1234.5678,2) AS TRUNC_2, -- 소수점 3번째 버림 후 출력                              
TRUNC(1234.5678,-1) AS TRUNC_MINUS1, -- 1의 자리를 버림 후 출력                               
TRUNC(1234.5678,-2) AS TRUNC_MINUS2 -- 10의 자리를 버림 후 출력                                         
FROM DUAL;

SELECT CEIL(3.14), -- CEIL 가장 가까운 큰 정수 출력                                            
FLOOR(3.14), -- FLOOR 가장 가까운 작은 정수 출력                                              
CEIL(-3.14),                                                                                               
FLOOR(-3.14)                                                                                     
FROM DUAL;                                                                                             

SELECT MOD(15,6), -- 나머지 값 출력.                                                                       
MOD(10,2),                                                                                         
MOD(11,2)                                                                             
FROM DUAL;
```

## 날짜 데이터를 다루는 날짜 함수
```SQL
ADD_MONTHS(날짜,개월)  : 몇 개월 이후 날짜                                                                   
MONTHS_BETWEEN(날짜,날짜) : 두 날짜 간의 개월수 차이                                                     
NEWT_DAY(날짜,요일) : 돌아오는 요일                                                                 
LAST_DAY(날짜) : 달의 마지막 날짜                                                     
ROUND, TURNC(숫자,위치) : 날짜의 반올림 , 버림                                                       

select * from emp where upper(ename) like upper('%s%');                                              
SELECT SYSDATE AS NOW, SYSDATE+1 AS TOMORROW FROM DUAL;                                               
SELECT ADD_MONTHS(SYSDATE,12) AS MON FROM DUAL;                                             

SELECT SYSDATE AS NOW, -- SYSDATE 현재 날짜.                                                      
SYSDATE -1 AS YESTERDAY, --SYSDATE -1 음수만큼 앞 날자 출력                                          
SYSDATE +1 AS TOMORROW -- SYSDATE +1 양수만큼 앞 날자 출력                                        
FROM DUAL; -- 임시로 결과 확인                                                  

SELECT SYSDATE, ADD_MONTHS(SYSDATE,-3) FROM DUAL;                                           
-- 월 단위로 음수만큼 뒤로 간다.       

SELECT EMPNO,ENAME,HIREDATE, ADD_MONTHS(HIREDATE,120) AS WORK10YEAR FROM EMP;                                      
-- HIREDATE를 WORK10YEAR 이름으로 +120개월 출력                                      
 
SELECT EMPNO,HIREDATE,SYSDATE FROM EMP WHERE ADD_MONTHS(HIREDATE,460)>SYSDATE;                            
-- SYSDATE로 부터 HIREDATE가 460개월 안되는 EMPNO 출력                  

SELECT SYSDATE,ADD_MONTHS(SYSDATE,6) FROM DUAL;                                                  
-- 오늘부터 6개월 뒤에 날자 출력                       

SELECT EMPNO,ENAME,HIREDATE,SYSDATE,                                                                      
MONTHS_BETWEEN(HIREDATE,SYSDATE) AS MONTHS1,                                                                  
MONTHS_BETWEEN(SYSDATE, HIREDATE) AS MONTHS2,                                                        
TRUNC(MONTHS_BETWEEN(SYSDATE,HIREDATE)) AS MONTH3                                                
FROM EMP;                                                                                  
-- 두 날짜 데이터 간의 날짜 차이를 개월수로 계산하여 출력.                                               

SELECT SYSDATE,                                                                       
NEXT_DAY(SYSDATE,'금'),                                                                         
LAST_DAY(SYSDATE)                                                                          
FROM DUAL;                                                                 

SELECT SYSDATE,                                                                             
ROUND(SYSDATE-10,'CC') AS FORMAT_CC,                                                                   
ROUND(SYSDATE-10,'YYYY') AS FORMAT_YYYY,                                                               
ROUND(SYSDATE-10,'Q') AS FORMAT_Q,                                                                      
ROUND(SYSDATE-10,'DDD') AS FORMAT_DDD,                                                                        
ROUND(SYSDATE-10,'HH') AS FORMAT_HH                                                                           
FROM DUAL;

SELECT SYSDATE,                                                                                      
TRUNC(SYSDATE-10,'CC') AS FORMAT_CC,                                                                 
TRUNC(SYSDATE-10,'YYYY') AS FORMAT_YYYY,                                                                      
TRUNC(SYSDATE-10,'Q') AS FORMAT_Q,                                                                        
TRUNC(SYSDATE-10,'DDD') AS FORMAT_DDD,                                                                    
TRUNC(SYSDATE-10,'HH') AS FORMAT_HH                                                                           
FROM DUAL;      
```

## 자료형을 변환하는 형 변환 함수
```SQL
TO_CHAR(데이터) : 숫자 또는 날짜 데이터를 문자 데이터로 변환
TO_NUMBER(데이터) : 문자 데이터를 숫자 데이터로 변환
TO_DATE(데이터) :  문자 데이터를 날짜 데이터로 변환

SELECT EMPNO,ENAME,EMPNO+'500' FROM EMP WHERE ENAME = 'SMITH';
--숫자형 문자를 자동형 변환을 하여 기존 숫자에 더해줌

SELECT 'ABCD'+EMPNO,EMPNO FROM EMP WHERE ENAME = 'JAMES';
-- 문자형 문자를 숫자에 더하기 때문에 형변환이 일어나지 않고 오류가 발생.

SELECT TO_CHAR(SYSDATE,'YYYY/MM/DD HH24:MI:SS')AS 현재날짜시간 FROM DUAL;
-- 2020/월/날짜 시:분:초 출력

SELECT SYSDATE,
TO_CHAR(SYSDATE,'MM')AS MM,                                                         
TO_CHAR(SYSDATE,'MON')AS MON,                                                                
TO_CHAR(SYSDATE,'MONTH')AS MONTH,-- 월                                                            
TO_CHAR(SYSDATE,'DD')AS DD,                                                                
TO_CHAR(SYSDATE,'DY')AS DY,                                                       
TO_CHAR(SYSDATE,'DAY')AS DAY -- 일                                                               
FROM DUAL;

-- 9는 숫자의 한자리 의미 빈공간 생성
-- 0은 빈자리를 0으로 채움
-- $ 달러 표시 후 출력
-- L 지역 화폐단위 표시
-- . 소수점 표시
-- , 천단위 기호 표시

SELECT SAL,
TO_CHAR(SAL,'$999,999') AS SAL_$,
TO_CHAR(SAL,'L999,999') AS SAL_L,
TO_CHAR(SAL,'999,999.00') AS SAL_1,
TO_CHAR(SAL,'000,999,999,00') AS SAL_2,
TO_CHAR(SAL,'0009999999,999') AS SAL_3,
TO_CHAR(SAL,'999,999,999,000') AS SAL_4
FROM EMP;

SELECT TO_NUMBER('1,300','9999')-TO_NUMBER('1,500','9999') FROM DUAL;

SELECT TO_DATE('49/12/10','YY/MM/DD') AS YY_YEAR_49,
TO_DATE('49/12/10','RR/MM/DD') AS RR_YEAR_49,
TO_DATE('49/12/10','YY/MM/DD') AS YY_YEAR_50,
TO_DATE('49/12/10','RR/MM/DD') AS RR_YEAR_50,
TO_DATE('49/12/10','YY/MM/DD') AS YY_YEAR_51,
TO_DATE('49/12/10','RR/MM/DD') AS RR_YEAR_51
FROM DUAL;
```

## NULL 처리 함수
```SQL
--NVL(NULL인지 검사할 데이터 , NULL일경우 반환할 데이터)
--EX) NVL(COMM,0)
--NVL2(NULL인지 검사할 데이터 , NULL이 아닐경우 반환할 데이터 , NULL일겨우 반환할 데이터)
--EX) NVL(COMM,SAL*12+COMM,SAL*12) *계산식을 넣어도 된다.*

SELECT EMPNO,ENAME,SAL,COMM,SAL+COMM,NVL(COMM,0),SAL+NVL(COMM,0) FROM EMP;

SELECT EMPNO,ENAME,JOB,SAL,
DECODE(JOB,   -- 조건식
      'MANAGER',SAL*1.1,  -- 조건식에 일치한다면 SAL * 1.1 진행
      'SLAESMAN',SAL*1.05, -- 조건식에 일치한다면 SAL * 1.05 진행
      'ANALYST',SAL,   -- 조건식에 일치한다면 SAL 진행
      SAL*1.03)   -- 조건식에 나머지에 SAL * 1.03 진행
AS UPSAL FROM EMP;

SELECT EMPNO,ENAME,JOB,SAL,
CASE JOB -- 조건식
WHEN 'MANAGER' THEN SAL * 1.1    -- 조건식에 일치한다면 SAL * 1.1 진행
WHEN 'SALESMAN' THEN SAL * 1.05   -- 조건식에 일치한다면 SAL * 1.05 진행
WHEN 'ANALYST' THEN SAL           -- 조건식에 일치한다면 SAL 진행
ELSE SAL * 1.03                   -- 조건식에 나머지에 SAL * 1.03 진행
END AS UPSAL FROM EMP;

SELECT EMPNO,ENAME,COMM,
CASE
WHEN COMM IS NULL THEN '해당사항 없음'
WHEN COMM = 0 THEN '수업없음'
WHEN COMM > 0 THEN '수당:'||COMM
END AS COMM_TEXT
FROM EMP;
```

## 다중행 함수
```sql
-- 합계를 구하는 함수 SUM
select SAL from emp; --모든 SAL 출력
select sum(sal) from emp; --모든 SAL의 합 출력
SELECT SUM(COMM) FROM EMP; -- NULL 이 있어도 COMM의 합 출력 

SELECT SUM(DISTINCT SAL), -- 중복 값 제외한 SAL의 합 출력
SUM(ALL SAL), -- 모든 SAL 출력
SUM(SAL) -- 모든 SAL 출력
FROM EMP;
SELECT DISTINCT(SAL) FROM EMP; -- 중복된값 제외 하고 출력

-- 데이터 개수를 구하는 COUNT함수
SELECT COUNT(*) AS CNT30 FROM EMP WHERE DEPTNO = 30; -- 부서 번호 30번의 개수
SELECT COUNT(DISTINCT SAL), COUNT(ALL SAL), COUNT(SAL) FROM EMP; -- 중복 개수,모두 출력개수

SELECT COUNT(COMM) FROM EMP; --COMM의 개수 NULL은 세지 않음.
select count(comm) from emp where comm is null; -- NULL을 세지 않아서 0개 출력.
-- COUNT 함수는 NULL 데이터는 반환개수에서 제외 시킴.

--최대,최소 값을 반환하는 MAX,MIN 함수
SELECT MAX(SAL) FROM EMP WHERE DEPTNO = 10; -- 최대 SAL 값 5000출력
SELECT MIN(SAL) FROM EMP WHERE DEPTNO = 10; -- 최소 SAL 값 1300출력
SELECT MAX(HIREDATE) FROM EMP WHERE DEPTNO = 20; -- 가장늦게 입사일 출력
SELECT MIN(HIREDATE) FROM EMP WHERE DEPTNO = 20;-- 가장 빠른 입사일 출력

--평균 값을 반환하는 AVG 함수
SELECT AVG(SAL) FROM EMP WHERE DEPTNO = 30; --30번 부서의 평균 출력
SELECT AVG(DISTINCT SAL) FROM EMP WHERE DEPTNO = 30; --중복값을 제외한 평균값 출력

SELECT AVG(SAL), '10' AS DEPTNO FROM EMP WHERE DEPTNO = 10
UNION ALL
SELECT AVG(SAL), '20' AS DEPTNO FROM EMP WHERE DEPTNO = 20
UNION ALL
SELECT AVG(SAL), '30' AS DEPTNO FROM EMP WHERE DEPTNO = 30;
-- 합집합을 사용하여 부서별로 평균 출력

-- 그룹을 묶어서 출력하는 방법.!
SELECT DEPTNO, AVG(SAL) FROM EMP GROUP BY DEPTNO; -- 그룹으로 묶어서 평균 출력

SELECT DEPTNO,JOB,AVG(SAL) FROM EMP
GROUP BY DEPTNO,JOB ORDER BY DEPTNO,JOB; -- 부서,직업별로 평균값 출력

SELECT DEPTNO,JOB,AVG(SAL) FROM EMP GROUP BY DEPTNO,JOB HAVING AVG(SAL) >= 2000
ORDER BY DEPTNO,JOB; -- SAL평균이 2000이상인 부서,직업만 출력

SELECT AVG(COMM), DEPTNO FROM EMP GROUP BY DEPTNO; -- 부서별로 추가수당 출력

--HAVING절은 '그룹화'된 대상을 출력에서 제한 한다.
--WHERE절은 출력 대상 '행'을 제한한다.
SELECT DEPTNO, JOB, AVG(SAL) FROM EMP WHERE AVG(SAL) >= 2000 -- 오류
GROUP BY DEPTNO, JOB ORDER BY DEPTNO, JOB; -- WHERE절은 GROUP BY를 제한 할수 없다.

SELECT DEPTNO, JOB, AVG(SAL) FROM EMP GROUP BY DEPTNO,JOB HAVING AVG(SAL) >= 2000 
ORDER BY DEPTNO, JOB; -- GROUP BY 제한한 HAVING 절

SELECT DEPTNO,JOB,AVG(SAL) FROM EMP WHERE SAL <= 3000 -- WHERE절이 행을 제한
GROUP BY DEPTNO,JOB HAVING AVG(SAL) >= 2000 -- 그룹화를 HAVING이 제한
ORDER BY DEPTNO,JOB; -- 정열을 시키는 ORDER BY

SELECT DEPTNO, JOB,AVG(SAL) FROM EMP GROUP BY DEPTNO,JOB HAVING AVG(SAL) >= 500
ORDER BY DEPTNO,JOB; -- SAL의 평균이 500이상인 부서,직업 출력
```

## rollup(a, b, c) 함수
```sql
--1. a , b, c 그룹에 해당하는 결과 출력
--2. a, b 그룹에 해당하는 결과 출력
--3. a 그룹에 해당하는 결과 출력
-- 전체 데이터 결과 출력

select deptno,job,count(*),max(sal),sum(sal),avg(sal) 
from emp -- select~ from 순서 대로 컬럼 이름 출력
group by deptno,job -- deptno , job 순서로 그룹화
order by deptno,job; -- deptno , job 순서대로 정렬

select deptno, job, count(*),max(sal),sum(sal),avg(sal)
from emp -- select~ from 순서 대로 컬럼 이름 출력
group by rollup(deptno,job);  -- deptno 기준으로 정렬
--동일하게 출력 후 부서마지막 마다 총 데이터 결과 출력

select deptno, job, count(*),max(sal),sum(sal),avg(sal)
from emp -- select~ from 순서 대로 컬럼 이름 출력
group by job ,rollup(deptno); -- job 기준으로 정렬, deptno 전체 출력

select deptno, job, count(*),max(sal),sum(sal),avg(sal)
from emp
group by deptno,rollup(job); -- deptno 기준으로 정렬, job 전체
```
## grouping sets함수
```sql
-- grouping sets(a,b) / a는 a 끼리 b는 b끼리 한번에 출력
select deptno, job, count(*),max(sal),sum(sal),avg(sal)
from emp
group by grouping sets(deptno,job) --deptno 출력 후 job 출력
order by deptno,job;


select * from emp,dept --from 절에 테이블 여러개 선언
where emp.deptno = dept.deptno -- where 설정 안하면 중복 값 출력
order by empno; -- empno 기준으로 정렬
```
## 테이블의 별칭 설정
```sql
select * from emp E,dept D -- 테이블 별칭 , 테이블1 별칭1
where E.deptno = D.deptno -- 중복 제거를 위한 식
order by empno;

select E.empno,E.ename, D.deptno,D.dname,D.loc  -- 테이블 별칭을 먼저
from emp E,DEPT D -- 테이블 별칭 생성
where E.deptno = D.deptno -- 중복 제거
order by D.deptno,E.deptno;

select * from salgrade; -- salgrade 필드 보기.

select * from emp E, salgrade S -- 별칭 생성
where E.sal between S.losal and S.hisal; -- 별칭을 이용한 조건식

select * from emp;
```
## 자체 조인, 외부 조인
```sql
select E1.empno, E1.ename, E1.mgr,
E2.empno as mgr_empno,
E2.ename as mgr_ename
from emp E1, emp E2
where E1.mgr = E2.empno
order by E1.empno;

select E1.empno, E1.ename, E1.mgr,
E2.empno as mgr_empno,
E2.ename as mgr_ename
from emp E1, emp E2
where E1.mgr = E2.empno(+)
order by E1.empno;

select E1.empno, E1.ename, E1.mgr,
E2.empno as mgr_empno,
E2.ename as mgr_ename
from emp E1, emp E2
where E1.mgr(+) = E2.empno
order by E1.empno;

select E.empno, E.ename, E.job, E.mgr, E.hiredate, E.sal, E.comm, deptno, d.dname, d.loc
from emp E natural join dept D
order by deptno, E.empno;

select e.empno, e.ename, e.job, e.mgr, e.hiredate, e.sal, e.comm, deptno, d.dname, d.loc
from emp e join dept d using (deptno)
where sal >=3000
order by deptno, e.empno;

select e.empno, e.ename, e.job, e.mgr, e.hiredate, e.sal, e.comm, e.deptno, d.dname, d.loc
from emp e join dept d on(e.deptno = d.deptno)
where sal <=3000
order by e.deptno, empno;

select e1.empno, e1.ename, e1.mgr, e2.empno as mgr_empno, e2.ename as mgr_ename
from emp e1 join emp e2 on (e1.mgr = e2.empno)
order by e1.deptno;

```
