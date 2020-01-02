# SQL

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

## 날짜 데이터를 다루는 날짜 함수

ADD_MONTHS  : 몇 개월 이후 날짜                                                                   
MONTHS_BETWEEN : 두 날짜 간의 개월수 차이                                                     
NEWT_DAY : 돌아오는 요일                                                                 
LAST_DAY : 달의 마지막 날짜                                                     
ROUND, TURNC : 날짜의 반올림 , 버림                                                       

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
