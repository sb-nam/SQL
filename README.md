# SQL

select Ename,upper(ename),lower(ename),initcap(ename) from emp; -- 대소문자 구분

select * from emp where upper(ename) like upper('%smith%'); 
select * from emp where upper(ename)=upper('smith'); -- 대문자로 이름 변경

select initcap(ename) from emp;

select ename,length(ename) from emp;
