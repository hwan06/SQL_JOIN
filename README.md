# 내부 조인
### 내부 조인이란 각 테이블에서 동일한 데이터 값을 이용하여 테이블을 연결해주는 조인 방식이다.
### J-1) 급여가 3000이상인 사원번호, LAST_NAME, SALARY, 부서명, 도시명을 조회하시오.    
SELECT E.EMPLOYEE_ID, E.LAST_NAME, E.SALARY, D.DEPARTMENT_NAME, L.CITY      
FROM EMPLOYEES E, DEPARTMENTS D, LOCATIONS L      
WHERE E.DEPARTMENT_ID = D.DEPARTMENT_ID AND D.LOCATION_ID = L.LOCATION_ID      
AND E.SALARY >= 3000;    

---   

J-2) 급여가 2500 이하이고 사원번호가 200이하인 사원의 LAST_NAME, 부서명을 조회하시오.       
SELECT E.LAST_NAME, D.DEPARTMENT_NAME    
FROM EMPLOYEES E, DEPARTMENTS D       
WHERE E.DEPARTMENT_ID = D.DEPARTMENT_ID AND SALARY <= 2500 AND EMPLOYEE_ID <= 200;  

---    
# 비등가조인 
### 비등가조인이란 연결할 테이블의 데이터만 필요할때 사용하는 것으로 등호(=)표시가 없는것이 특징이다.
### J-3) 급여범위가 JOBS 테이블의 최소급여(MIN_SALARY)와 최대 급여(MAX_SALARY) 사이에 있는 사원의 LAST_NAME, JOB_ID를 조회하시오.    

SELECT E.LAST_NAME, J.JOB_ID      
FROM EMPLOYEES E, JOBS J      
WHERE E.SALARY BETWEEN J.MIN_SALARY AND J.MAX_SALARY;     

---
# 셀프조인
### 셀프조인이란 같은 테이블을 다른 테이블처럼 두개의 복제품을 만들어 서로 조인하여 사용하는 방식이다.
### J-4) 자신의 매니저보다 먼저 고용된 사원들의 LAST_NAME 및 고용일을 조회한다.   
SELECT EMP.LAST_NAME, EMP.HIRE_DATE    
FROM EMPLOYEES EMP, EMPLOYEES MGR    
WHERE EMP.MANAGER_ID = MGR.EMPLOYEE_ID AND EMP.HIRE_DATE < MGR.HIRE_DATE;     

---
# 셀프조인(내부 조인)
### 내부 조인이란 같은 값이 존재할 경우에만 레코드를 출력하는 경우를 말한다. 
### 예를 들면 밑에 예시문에서 사원의 매니저가 없다면 값이 출력되지 않는다.
### J-5) 사원정보(EMPLOYEE_ID, LAST_NAME, MANAGER_ID)와 사원의 직속 상관정보(EMPLOYEE_ID, LAST_NAME)를 조회하시오.    

   
---
# 셀프조인(외부 조인)
### J-5) 사원정보(EMPLOYEE_ID, LAST_NAME, MANAGER_ID)와 사원의 직속 상관정보(EMPLOYEE_ID, LAST_NAME)를 조회하시오.    
### 외부조인이란 같은 값이 존재하지 않을경우 null값을 출력한다.
### 예를 들어 밑에 예시문에서 사원의 매니저가 없다면 내부조인과는 다르게 null값을 출력한다.
SELECT EMP.EMPLOYEE_ID AS 사원번호, EMP.LAST_NAME AS 사원이름, EMP.MANAGER_ID AS 사원의매니저번호, MGR.EMPLOYEE_ID AS 매니저의사원번호, MGR.LAST_NAME AS 매니저의이름    
FROM EMPLOYEES EMP, EMPLOYEES MGR    
WHERE EMP.MANAGER_ID = MGR.EMPLOYEE_ID(+) -- 왼쪽 외부조인    
ORDER BY EMP.EMPLOYEE_ID;    
