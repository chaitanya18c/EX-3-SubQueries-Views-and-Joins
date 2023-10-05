# EX 3 SubQueries, Views and Joins 


## Create employee Table
```sql
CREATE TABLE EMP (EMPNO NUMBER(4) PRIMARY KEY,ENAME VARCHAR2(10),JOB VARCHAR2(9),MGR NUMBER(4),HIREDATE DATE,SAL NUMBER(7,2),COMM NUMBER(7,2),DEPTNO NUMBER(2));
```
## Insert the values
```sql
INSERT INTO EMP (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES (7369, 'SMITH', 'CLERK', 7902, '17-DEC-80', 800, NULL, 20);

INSERT INTO EMP (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES (7499, 'ALLEN', 'SALESMAN', 7698, '20-FEB-81', 1600, 300, 30);

INSERT INTO EMP (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES (7521, 'WARD', 'SALESMAN', 7698, '22-FEB-81', 1250, 500, 30);

INSERT INTO EMP (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES (7566, 'JONES', 'MANAGER', 7839, '02-APR-81', 2975, NULL, 20);

INSERT INTO EMP (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES (7654, 'MARTIN', 'SALESMAN', 7698, '28-SEP-81', 1250, 1400, 30);

INSERT INTO EMP (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES (7698, 'BLAKE', 'MANAGER', 7839, '01-MAY-81', 2850, NULL, 30);

INSERT INTO EMP (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES (7782, 'CLARK', 'MANAGER', 7839, '09-JUN-81', 2450, NULL, 10);

INSERT INTO EMP (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES (7788, 'SCOTT', 'ANALYST', 7566, '19-APR-87', 3000, NULL, 20);

INSERT INTO EMP (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES (7839, 'KING', 'PRESIDENT', NULL, '17-NOV-81', 5000, NULL, 10);

INSERT INTO EMP (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES (7844, 'TURNER', 'SALESMAN', 7698, '08-SEP-81', 1500, 0, 30);

INSERT INTO EMP (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES (7876, 'ADAMS', 'CLERK', 7788, '23-MAY-87', 1100, NULL, 20);

INSERT INTO EMP (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES (7900, 'JAMES', 'CLERK', 7698, '03-DEC-81', 950, NULL, 30);

INSERT INTO EMP (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES (7902, 'FORD', 'ANALYST', 7566, TO_DATE('03-DEC-81', 'DD-MON-RR'), 3000, 20, 20);

INSERT INTO EMP (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES (7934, 'MILLER', 'CLERK', 7782, TO_DATE('23-JAN-82', 'DD-MON-RR'), 1300, 10, 10);
```

## Create department table
```sql
CREATE TABLE DEPT (DEPTNO NUMBER(2) PRIMARY KEY,DNAME VARCHAR2(14),LOC VARCHAR2(13));
```
## Insert the values in the department table
```sql
INSERT INTO DEPT (DEPTNO, DNAME, LOC) VALUES (10, 'ACCOUNTING', 'NEW YORK');

INSERT INTO DEPT (DEPTNO, DNAME, LOC) VALUES (20, 'RESEARCH', 'DALLAS');

INSERT INTO DEPT (DEPTNO, DNAME, LOC) VALUES (30, 'SALES', 'CHICAGO');

INSERT INTO DEPT (DEPTNO, DNAME, LOC) VALUES (40, 'OPERATIONS', 'BOSTON');
```

### Q1) List the name of the employees whose salary is greater than that of employee with empno 7566.


### QUERY:
SELECT ename FROM EMP WHERE sal > (SELECT sal FROM EMP WHERE empno = 7566);

### OUTPUT:
![272034736-44b9339b-81e2-428c-be17-d2604c016589](https://github.com/chaitanya18c/EX-3-SubQueries-Views-and-Joins/assets/119392724/646ff730-877c-4cd5-90b8-f8c39f943d60)

### Q2) List the ename,job,sal of the employee who get minimum salary in the company.

### QUERY:
SELECT ename,job,sal FROM EMP WHERE sal = (SELECT MIN(sal) FROM EMP);



### OUTPUT:
![272035101-cd7c9d83-56b9-4b37-8a1e-569fbaf63c91](https://github.com/chaitanya18c/EX-3-SubQueries-Views-and-Joins/assets/119392724/9bee1e13-9b49-43f2-abbf-a17787d4a033)

### Q3) List ename, job of the employees who work in deptno 10 and his/her job is any one of the job in the department ‘SALES’.

### QUERY:
SELECT ename,job FROM EMP WHERE deptno = 10 AND job IN (SELECT job FROM EMP WHERE job = 'sales');

### OUTPUT:
![272035151-6dbe5796-8f8f-4319-a5f2-9a5a982fedce](https://github.com/chaitanya18c/EX-3-SubQueries-Views-and-Joins/assets/119392724/ff6439b0-2c92-4afd-92a0-5e248b137f45)


### Q4) Create a view empv5 (for the table emp) that contains empno, ename, job of the employees who work in dept 10.

### QUERY:
create view empv5 as select EMPNO,ENAME,JOB from EMP where DEPTNO=10; SELECT * FROM empv5;



### OUTPUT:
![272035377-c88ff806-ff24-45fe-bc61-77e2029ed631](https://github.com/chaitanya18c/EX-3-SubQueries-Views-and-Joins/assets/119392724/695fbb45-64db-4211-bbd0-d1095c4576e2)

### Q5) Create a view with column aliases empv30 that contains empno, ename, sal of the employees who work in dept 30. Also display the contents of the view.

### QUERY:
create view empv30 AS select EMPNO,ENAME,SAL from EMP where DEPTNO=30; SELECT * FROM empv30;



### OUTPUT:
![272035484-36a4a32a-36a6-4288-8160-98b68e81d0fa](https://github.com/chaitanya18c/EX-3-SubQueries-Views-and-Joins/assets/119392724/7bbe9ead-fb27-4a10-9d33-3bf857f89b84)


### Q6) Update the view empv5 by increasing 10% salary of the employees who work as ‘CLERK’. Also confirm the modifications in emp table

### QUERY:
UPDATE EMP SET sal = sal * 1.1 WHERE job = 'CLERK'; create view empv5 as select EMPNO,ENAME,SALARY,JOB from EMP;



### OUTPUT:
![272035559-6de5c7e8-4d65-4749-9275-a6b8940acdfd](https://github.com/chaitanya18c/EX-3-SubQueries-Views-and-Joins/assets/119392724/36179ac3-24e8-41a2-86aa-8b1861be2163)


## Create a Customer1 Table
```sql
CREATE TABLE Customer1 (customer_id INT,cust_name VARCHAR(20),city VARCHAR(20),grade INT,salesman_id INT);
```
## Inserting Values to the Table
```sql
INSERT INTO Customer1 (customer_id, cust_name, city, grade, salesman_id) VALUES(3002, 'Nick Rimando', 'New York', 100, 5001);
INSERT INTO Customer1 (customer_id, cust_name, city, grade, salesman_id) VALUES(3007, 'Brad Davis', 'New York', 200, 5001);
INSERT INTO Customer1 (customer_id, cust_name, city, grade, salesman_id) VALUES(3005, 'Graham Zusi', 'California', 200, 5002);
INSERT INTO Customer1 (customer_id, cust_name, city, grade, salesman_id) VALUES(3008, 'Julian Green', 'London', 300, 5002);
INSERT INTO Customer1 (customer_id, cust_name, city, grade, salesman_id) VALUES(3004, 'Fabian Johnson', 'Paris', 300, 5006);
INSERT INTO Customer1 (customer_id, cust_name, city, grade, salesman_id) VALUES(3009, 'Geoff Cameron', 'Berlin', 100, 5003);
INSERT INTO Customer1 (customer_id, cust_name, city, grade, salesman_id) VALUES(3003, 'Jozy Altidor', 'Moscow', 200, 5007);
INSERT INTO Customer1 (customer_id, cust_name, city, grade, salesman_id) VALUES(3001, 'Brad Guzan', 'London', NULL, 5005);
```
## Create a Salesperson1 table
```sql
CREATE TABLE Salesman1 (salesman_id INT,name VARCHAR(20),city VARCHAR(20),commission DECIMAL(4,2));
```
## Inserting Values to the Table
```sql
INSERT INTO Salesman1 (salesman_id, name, city, commission) VALUES(5001, 'James Hoog', 'New York', 0.15);
INSERT INTO Salesman1 (salesman_id, name, city, commission) VALUES(5002, 'Nail Knite', 'Paris', 0.13);
INSERT INTO Salesman1 (salesman_id, name, city, commission) VALUES(5005, 'Pit Alex', 'London', 0.11);
INSERT INTO Salesman1 (salesman_id, name, city, commission) VALUES(5006, 'Mc Lyon', 'Paris', 0.14);
INSERT INTO Salesman1 (salesman_id, name, city, commission) VALUES(5007, 'Paul Adam', 'Rome', 0.13);
INSERT INTO Salesman1 (salesman_id, name, city, commission) VALUES(5003, 'Lauson Hen', 'San Jose', 0.12);
```
### Q7) Write a SQL query to find the salesperson and customer who reside in the same city. Return Salesman, cust_name and city.

### QUERY:
select s.name,c.cust_name,s.city from salesman1 s ,customer1 c where s.city=c.city;



### OUTPUT:
![272035646-4bbb2ccd-0234-435e-b50d-a174e26f388d](https://github.com/chaitanya18c/EX-3-SubQueries-Views-and-Joins/assets/119392724/e040d784-bdf4-4b97-b955-51e1e11a72c7)


### Q8) Write a SQL query to find salespeople who received commissions of more than 13 percent from the company. Return Customer Name, customer city, Salesman, commission.


### QUERY:
select s.name,c.cust_name,c.city,s.commission from salesman1 s inner join customer1 c on s.city=c.city where s.commission>0.13;

### OUTPUT:
![272035667-7188fa42-dde7-4879-b3c7-973188ef7e12](https://github.com/chaitanya18c/EX-3-SubQueries-Views-and-Joins/assets/119392724/9e9e8d40-b2f2-4633-92f5-70bbf5917546)

### Q9) Perform Natural join on both tables

### QUERY:
select * from salesman1 s natural join customer1 c;

### OUTPUT:
![272035716-f7edfee9-fa69-465c-b03b-12109ab79ea0](https://github.com/chaitanya18c/EX-3-SubQueries-Views-and-Joins/assets/119392724/149a3353-3ea3-42f0-a1c0-432201f0d2db)

### Q10) Perform Left and right join on both tables

### QUERY:
select s.name,c.cust_name,c.city,s.commission from salesman1 s left join customer1 c on s.salesman_id=c.salesman_id; select s.name,c.cust_name,c.city,s.commission from salesman1 s right join customer1 c on s.salesman_id=c.salesman_id;

### OUTPUT:
## LEFT JOIN:
![272036922-1e3ba918-8b29-4f0d-8d11-27802b45f2d8](https://github.com/chaitanya18c/EX-3-SubQueries-Views-and-Joins/assets/119392724/9bd094b7-5017-42da-96a8-e86a66c72b50)


## RIGHT JOIN:
![272036433-be2ab519-52ad-44d7-8ee8-304c33ecb180](https://github.com/chaitanya18c/EX-3-SubQueries-Views-and-Joins/assets/119392724/168a0760-801f-4aed-907c-0dfd36896c8c)


### RESULT:
Thus to create a database and implementation of views,subqueries and joins is executed successfully.
