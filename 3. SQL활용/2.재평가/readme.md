# SQL 평가문제

## 1. `project_data`라는 테이블스페이스를 생성하는 SQL을 작성하시오.
- 데이터파일 경로: `C:/Data/project_data.dbf`
- 크기: `20MB`

---

## 2. 사용자 계정 `HR`의 비밀번호를 `hrSecure!456`으로 변경하는 SQL을 작성하시오.

---

## 3. 현재 데이터베이스에 존재하는 테이블스페이스 목록을 조회하는 SQL을 작성하시오.

---

## 4. 다음 속성을 가지는 `departments_demo` 테이블을 생성하시오.
- 부서번호(department_id: `NUMBER(4)`, 기본키)
- 부서명(department_name: `VARCHAR2(50)`)
- 지역코드(location_id: `NUMBER(4)`)

---

## 5. `job_id`가 `'IT_PROG'` 또는 `'SA_REP'`인 사원만을 조회하는 `it_sales` 뷰(View)를 생성하시오.
- 컬럼: `employee_id`, `first_name`, `job_id`

---

## 6. `orders` 테이블에서 다음 제약조건을 추가하시오.
- `amount` 컬럼은 1 이상만 가능
- `order_date` 컬럼은 NULL을 허용하지 않도록 수정

---

## 7. `orders` 테이블과 `customers` 테이블을 조인하여, 주문번호와 고객명을 조회하시오.
- orders(order_id, customer_id)
- customers(customer_id, customer_name)

---

## 8. 직원 중 평균 연봉보다 높은 연봉을 받는 직원의 이름(name)과 연봉(salary)을 조회하시오.

---

## 9. 부서번호가 20이고 평균 연봉보다 낮은 직원의 연봉을 15% 인상하시오.

---

## 10. 직원 테이블에서 퇴사여부가 `'Y'`로 표시된 직원들을 삭제하시오.
- employees(emp_id, name, resign_flag)
