# [mySQL]
## Select from ~where,like,between,orderby 까지 활용한 문제 학습

- select 는 검색의 기능을 갖추고 있으며 from 테이블명을 입력하면 해당 태이블에 대한 정보검색이 가능하다.
- where는 조회하는 결과에 특정한 조건을 부여하여 전체 데이터 이외 원하는 데이터를 보고자할 때 
  사용한다.
- like는  주로 특정 문자열을 포함한 데이터만 열람할 때 쓰인다.
- order by는 데이터를 정렬하는 기능이 있으며, 오름차순은 ASC /내림차순은 DESC로 가능하다.
  =>  order by는 ASC/DESC 둘 중 하나는 반드시 입력해주어야 실행가능하다.
  * 또한 select -> from -> where-> Group by ->having -> order by 순 임을 기억하자!
    비록 전에 sqld 자격증 시험은 떨어졌지만..정보처리기사도 그렇고 공부해놓은 베이스가
    있어서 정신줄 놓지 않고 따라갈 수 있는 것 같다 ㅠㅠ
- BETWEEN은  영단어에서도 Between A and B 숙어처럼 SQL 에서도 BETWEEN AND가 사용된다.
  그리고 반대의 의미를 나타낼 때는 NOT BETWEEN을 입력하면 된다.
- NULL의 경우 회사생활에서 자주 보인 친숙한 언어인데, 데이터가 정의되는 않은 상태로
  존재하며, 값이 있는 숫자와 NULL을 계산해도 NULL이다.
  * 열심히 공부하고 복습하면서 sqld도 재도전해볼것이다! 화이팅!

#1.급여가 12,000 넘는 사원 이름, 급여 표시하는 query
~~~
select last_name, salary   #사원의 이름과 급여를 표시해야하므로 검색 내용에 입력한다.
from employees             #employees 테이블에서 가져오기
where salary>=12000 ;      #특정조건 : salary가 12000이상인 salary 데이터만 가져와라.
   
~~~
#2. 사원 번호가 176인 사원의 이름과 부서 번호를 표시하는 query

~~~
select employee_id, last_name, department_id
from employees
where employee_id =176 ;
~~~

#3.급여가 5000에서 12000 사이에 포함되지 않는 모든 사원의 이름과 급여를 표시하는 query

~~~
select last_name, salary
from employees
where salary NOT BETWEEN 5000 and 12000 ;
~~~
#4.2005년 2.20 과 2005.05.01 사이에 입사한 사원의 이름. 업무id 및 시작일을 표시하되, 시작일을
기준으로 오름차순으로 정렬

~~~
select last_name, job_id, hire_date
from employees
where hire_date between '2005-02-20' and '2005-05-01'
order by hire_date ASC;
~~~
#5. 부서 20 및 50에 속하는 모든 사원의 이름과 부서번호 이름을 기준으로 영문자순으로 표기 

~~~
select department_id , last_name, department_name
from employees
natural join departments
where department_id between 20 and 50
~~~

#6. 급여가 5000과 12000사이고 부서번호가 20또는 50인 사원의 이름과 급여 표기 

~~~
select department_id, last_name, salary
from employees
where salary between 5000 and 12000 and department_id between 20 and 50
order by department_id asc;
~~~

#7. 2007년에 입사한 모든 사원의 이름과 입사일을 표기 

~~~
select last_name, hire_date
from employees
where hire_date between '2007-01-01'and '2007-12-31'
~~~

#8.관리자가 없는 모든 사원의 이름과 업무를 표시. 

~~~
select last_name, job_id
from employees
where manager_id is null;
~~~

#9.커미션을 받는 모든 사원의 이름, 급여 및 커미션을 급여 및 커미션 기준으로 내림차순으로 정렬

~~~
select last_name, salary, commission_pct
from employees
where salary and commission_pct
order by salary and commission_pct DESC ;
~~~

#10.이름이 세번째 문자가 a인 모든 사원의 이름을 표시하십시오.

~~~
select last_name
from employees
where last_name like '__a%' ;   
~~~

#11.이름에 a와e가 있는 모든 사원의 이름을 표시하십시오.

~~~
select last_name
from employees
where last_name like '%a' and last_name like '%e%'
~~~

#12.업무가 영업사원 또는 사무원이면서 급여가 2500 또는 3500또는 7000가 아닌 모든 사원의 이름, 업무 및 급여를 표시 

~~~
select last_name, job_id, salary
from employees
where job_id like '%CLERK%' or '%REP%' and salary not between 2500 and 3500 and 7000
order by salary ASC;
~~~
