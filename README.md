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
