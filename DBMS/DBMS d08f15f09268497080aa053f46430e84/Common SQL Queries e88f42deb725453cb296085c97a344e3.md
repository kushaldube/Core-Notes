# Common SQL Queries

```sql
CREATE DATABASE ORG;
-- THIS IS A COMMENT 
SHOW DATABASES;
SHOW TABLES;
USE ORG;
 
CREATE TABLE WORKER (
	WORKER_ID INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
    FIRST_NAME VARCHAR(25),
    LAST_NAME VARCHAR(25),
    SALARY INT(15),	
    JOINING_DATE DATETIME,
    DEPARTMENT VARCHAR(25)
);

INSERT INTO WORKER (WORKER_ID, FIRST_NAME, LAST_NAME, SALARY, JOINING_DATE, DEPARTMENT)
VALUES (001, 'KUSHAL', 'DUBE', 100000, '14-02-20 09:00:00', 'HR'),
	(002, 'MONIKA', 'ARORA', 10000, '14-06-11 09:00:00', 'ADMIN'),
    (003, 'NIHARIKA', 'VERMA', 80000, '14-02-20 09:00:00', 'HR'),
    (004, 'VISHAL', 'SINGHAL', 300000, '14-02-20 09:00:00', 'ADMIN'),
    (005, 'AMITABH', 'SINGH', 500000, '14-06-11 09:00:00', 'ADMIN'),
    (006, 'VIVEK', 'DIWAN', 200000, '14-06-11 09:00:00', 'ACCOUNT'),
    (007, 'SATISH', 'KUMAR', 75000, '14-01-20 09:00:00', 'ACCOUNT'),
    (008, 'GEETIKA', 'CHAUHAN', 90000, '14-04-11 09:00:00', 'ADMIN');

SELECT * FROM WORKER;

CREATE TABLE BONUS (
	WORKER_REF_ID INT,
    BONUS_AMOUNT INT(10),
    BONUS_DATE DATETIME,
    FOREIGN KEY (WORKER_REF_ID)
		REFERENCES WORKER(WORKER_ID)
        ON DELETE CASCADE
);

INSERT INTO BONUS (WORKER_REF_ID, BONUS_AMOUNT, BONUS_DATE)
VALUES (001, 5000, '16-02-20'),
	(002, 3000, '16-06-11'),
    (003, 4000, '16-02-20'),
    (001, 4500, '16-02-20'),
    (002, 3500, '16-06-11');
    
SELECT * FROM BONUS;

CREATE TABLE TITLE (
	WORKER_REF_ID INT,
    WORKER_TITLE VARCHAR(25),
    AFFECTED_FROM DATETIME,
    FOREIGN KEY (WORKER_REF_ID)
		REFERENCES WORKER(WORKER_ID)
        ON DELETE CASCADE
);

INSERT INTO TITLE (WORKER_REF_ID, WORKER_TITLE, AFFECTED_FROM)
VALUES (001, 'MANAGER', '2016-02-20 00:00:00'),
	(002, 'EXECUTIVE', '2016-06-11 00:00:00'),
    (008, 'EXECUTIVE', '2016-06-11 00:00:00'),
    (005, 'MANAGER', '2016-06-11 00:00:00'),
    (004, 'ASST. MANAGER', '2016-06-11 00:00:00'),
    (007, 'EXECUTIVE', '2016-06-11 00:00:00'),
    (006, 'LEAD', '2016-06-11 00:00:00'),
    (003, 'LEAD', '2016-06-11 00:00:00');
    
SELECT * FROM TITLE;
```

```sql
-- Q-1. Write an SQL query to fetch "FIRST_NAME" from Worker table using the alias name as <WORKER_NAME>. 
SELECT FIRST_NAME AS WORKER_NAME FROM WORKER;

-- Q-2. Write an SQL query to fetch "FIRST_NAME" from Worker table in upper case and lower case.
SELECT UPPER(FIRST_NAME) FROM WORKER;
SELECT LOWER(FIRST_NAME) FROM WORKER;

-- Q-3. Write an SQL query to fetch unique values of DEPARTMENT from Worker table.
SELECT DISTINCT DEPARTMENT FROM WORKER;
SELECT DEPARTMENT FROM WORKER GROUP BY DEPARTMENT;

-- 0-4. Write an SQL query to print the first three characters of FIRST_NAME from Worker table.
SELECT SUBSTRING(FIRST_NAME, 1, 3) FROM WORKER;

-- Q-5. Write an SQL query to find the position of the alphabet ('b') in the first name column 'Amitabh' from Worker table.
SELECT INSTR(FIRST_NAME , "B") FROM WORKER WHERE FIRST_NAME='AMITABH';

-- Q-6. Write an SQL query to print the FIRST_NAME from Worker table after removing white spaces from the right side.
SELECT RTRIM(FIRST_NAME) FROM WORKER;

-- Q-7. Write an SQL query to print the DEPARTMENT from Worker table after removing white spaces from the left side.
SELECT LTRIM(FIRST_NAME) FROM WORKER;

-- Q-8. Write an SQL query that fetches the unique values of DEPARTMENT from Worker table and prints its length. 
SELECT DISTINCT DEPARTMENT, LENGTH(DEPARTMENT) FROM WORKER;

-- Q-9. Write an SQL query to print the FIRST_NAME from Worker table after replacing ‘a’ with ‘A’.
SELECT REPLACE(FIRST_NAME, 'A', 'a') FROM WORKER;

-- Q-10. Write an SQL query to print the FIRST_NAME and LAST_NAME from Worker table into a single column COMPLETE_NAME.
-- A space char should separate them.
SELECT CONCAT(FIRST_NAME, ' ', LAST_NAME) AS COMPLETE_NAME FROM WORKER;

-- Q-11. Write an SQL query to print all Worker details from the Worker table order by FIRST_NAME Ascending.
SELECT * FROM WORKER ORDER BY FIRST_NAME ASC;

-- Q-12. Write an SQL query to print all Worker details from the Worker table order by 
-- FIRST_NAME Ascending and DEPARTMENT Descending.
SELECT * FROM WORKER ORDER BY FIRST_NAME DESC;

-- Q-13. Write an SQL query to print details for Workers with the first name as “Vipul” and “Satish” from Worker table.
SELECT * FROM WORKER WHERE FIRST_NAME IN ('VIVEK', 'SATISH');

-- Q-14. Write an SQL query to print details of workers excluding first names, “Vipul” and “Satish” from Worker table.
SELECT * FROM WORKER WHERE FIRST_NAME NOT IN ('VIVEK', 'SATISH');

-- Q-15. Write an SQL query to print details of Workers with DEPARTMENT name as “Admin*”.
SELECT * FROM WORKER WHERE DEPARTMENT LIKE 'ADMIN%';

-- Q-16. Write an SQL query to print details of the Workers whose FIRST_NAME contains ‘a’.
SELECT * FROM WORKER WHERE FIRST_NAME LIKE '%A%';

-- Q-17. Write an SQL query to print details of the Workers whose FIRST_NAME ends with ‘a’.
SELECT * FROM WORKER WHERE FIRST_NAME LIKE '%A';

-- Q-18. Write an SQL query to print details of the Workers whose FIRST_NAME ends with ‘h’ and contains six alphabets.
SELECT * FROM WORKER WHERE FIRST_NAME LIKE '______H';

-- Q-19. Write an SQL query to print details of the Workers whose SALARY lies between 100000 and 500000.
SELECT * FROM WORKER WHERE SALARY BETWEEN 100000 AND 500000;

-- Q-20. Write an SQL query to print details of the Workers who have joined in Feb’2014.
SELECT * FROM WORKER WHERE YEAR(JOINING_DATE)=2014 AND MONTH(JOINING_DATE)=02;

-- Q-21. Write an SQL query to fetch the count of employees working in the department ‘Admin’.
SELECT DEPARTMENT, COUNT(*) AS COUNT FROM WORKER WHERE DEPARTMENT = 'ADMIN'; 

-- Q-22. Write an SQL query to fetch worker full names with salaries >= 50000 and <= 100000.
SELECT CONCAT(FIRST_NAME, ' ', LAST_NAME) AS FULL_NAME, SALARY FROM WORKER WHERE SALARY BETWEEN 50000 AND 100000;

-- Q-23. Write an SQL query to fetch the no. of workers for each department in the descending order.
SELECT DEPARTMENT, COUNT(WORKER_ID) AS COUNT FROM WORKER GROUP BY DEPARTMENT ORDER BY COUNT DESC;

-- Q-24. Write an SQL query to print details of the Workers who are also Managers.
SELECT W.* FROM WORKER AS W
INNER JOIN TITLE AS T
WHERE W.WORKER_ID = T.WORKER_REF_ID AND T.WORKER_TITLE='MANAGER';

-- Q-25. Write an SQL query to fetch number (more than 1) of same titles in the ORG of different types.
SELECT WORKER_TITLE, COUNT(*) AS COUNT FROM TITLE GROUP BY WORKER_TITLE HAVING COUNT>1 ;

-- Q-26. Write an SQL query to show only odd rows from a table.
SELECT * FROM WORKER WHERE MOD(WORKER_ID, 2)!=0;
SELECT * FROM WORKER WHERE MOD(WORKER_ID, 2)<>0;

-- Q-27. Write an SQL query to show only even rows from a table. 
SELECT * FROM WORKER WHERE MOD(WORKER_ID, 2)=0;

-- Q-28. Write an SQL query to clone a new table from another table.
CREATE TABLE WORKER_CLONE LIKE WORKER;
INSERT INTO WORKER_CLONE SELECT * FROM WORKER;
SELECT * FROM WORKER_CLONE;

-- Q-29. Write an SQL query to fetch intersecting records of two tables.
SELECT WORKER.* FROM WORKER
INNER JOIN WORKER_CLONE USING(WORKER_ID);	

-- Q-30. Write an SQL query to show records from one table that another table does not have.
-- MINUS
SELECT WORKER.* FROM WORKER
LEFT JOIN WORKER_CLONE USING(WORKER_ID)
WHERE WORKER_CLONE.WORKER_ID IS NULL;

-- Q-31. Write an SQL query to show the current date and time.
-- DUAL
SELECT CURDATE(); -- FORDATE
SELECT NOW(); -- DATE AND TIME

-- Q-32. Write an SQL query to show the top n (say 5) records of a table order by descending salary.
SELECT * FROM WORKER ORDER BY SALARY DESC LIMIT 5;

-- Q-33. Write an SQL query to determine the nth (say n=5) highest salary from a table.
SELECT * FROM WORKER ORDER BY SALARY DESC LIMIT 4,1; -- LIMIT N-1,1;

-- Q-34. Write an SQL query to determine the 5th highest salary without using LIMIT keyword.
SELECT SALARY FROM WORKER W1
WHERE 4= (
SELECT COUNT(DISTINCT (W2.SALARY))
FROM WORKER W2
WHERE W2.SALARY>=W1.SALARY
);
 
-- Q-35. Write an SQL query to fetch the list of employees with the same salary.
SELECT W1.* FROM WORKER W1, WORKER W2
WHERE W1.SALARY=W2.SALARY AND W1.WORKER_ID != W2.WORKER_ID;

-- Q-36. Write an SQL query to show the second highest salary from a table using sub-query.
SELECT SALARY FROM WORKER ORDER BY SALARY DESC LIMIT 1,1;
-- OR
SELECT MAX(SALARY) FROM WORKER
WHERE SALARY NOT IN (SELECT MAX(SALARY) FROM WORKER);

-- Q-37. Write an SQL query to show one row twice in results from a table.
SELECT * FROM WORKER
UNION ALL
SELECT * FROM WORKER
ORDER BY WORKER_ID;

-- Q-38. Write an SQL query to list worker_id who does not get bonus.
SELECT WORKER_ID FROM WORKER WHERE WORKER_ID NOT IN (SELECT WORKER_REF_ID FROM BONUS);

-- Q-39. Write an SQL query to fetch the first 50% records from a table.
SELECT * FROM WORKER WHERE WORKER_ID<= (SELECT COUNT(WORKER_ID)/2 FROM WORKER);

-- Q-40. Write an SQL query to fetch the departments that have less than 4 people in it.
SELECT DEPARTMENT,  COUNT(DEPARTMENT) AS DEPCOUNT FROM WORKER GROUP BY DEPARTMENT HAVING DEPCOUNT<4;

-- Q-41. Write an SQL query to show all departments along with the number of people in there.
SELECT DEPARTMENT,  COUNT(DEPARTMENT) AS DEPCOUNT FROM WORKER GROUP BY DEPARTMENT;

-- Q-42. Write an SQL query to show the last record from a table.
SELECT * FROM WORKER WHERE WORKER_ID = (SELECT MAX(WORKER_ID) FROM WORKER);

-- Q-43. Write an SQL query to fetch the first row of a table.
SELECT * FROM WORKER WHERE WORKER_ID = (SELECT MIN(WORKER_ID) FROM WORKER);

-- Q-44. Write an SQL query to fetch the last five records from a table.
(SELECT * FROM WORKER ORDER BY WORKER_ID DESC LIMIT 5) ORDER BY WORKER_ID;

-- Q-45. Write an SQL query to print the name of employees having the highest salary in each department.
SELECT W.DEPARTMENT, W.FIRST_NAME, W.SALARY FROM (SELECT MAX(SALARY) AS MAXSAL, DEPARTMENT FROM WORKER GROUP BY DEPARTMENT) AS TEMP
INNER JOIN
WORKER W ON TEMP.DEPARTMENT=W.DEPARTMENT AND TEMP.MAXSAL=W.SALARY;

-- Q-46. Write an SQL query to fetch three max salaries from a table using co-related subquery
SELECT DISTINCT SALARY FROM WORKER W1
WHERE 3>= (SELECT COUNT(DISTINCT SALARY) FROM WORKER W2 WHERE W1.SALARY <=W2.SALARY) ORDER BY W1.SALARY DESC;
-- DRY RUN AFTER REVISING THE CORELATED SUBQUERY CONCEPT FROM LEC-9.
SELECT DISTINCT SALARY FROM WORKER ORDER BY SALARY DESC LIMIT 3;

-- Q-47. Write an SQL query to fetch three min salaries from a table using co-related subquery
SELECT DISTINCT SALARY FROM WORKER W1
WHERE 3>= (SELECT COUNT(DISTINCT SALARY) FROM WORKER W2 WHERE W1.SALARY >=W2.SALARY) ORDER BY W1.SALARY DESC;

-- Q-48. Write an SQL query to fetch nth max salaries from a table.
SELECT DISTINCT SALARY FROM WORKER W1
WHERE N>= (SELECT COUNT(DISTINCT SALARY) FROM WORKER W2 WHERE W1.SALARY <=W2.SALARY) ORDER BY W1.SALARY DESC;

-- Q-49. Write an SQL query to fetch departments along with the total salaries paid for each of them.
SELECT DEPARTMENT, SUM(SALARY) AS DEPSAL FROM WORKER GROUP BY DEPARTMENT ORDER BY DEPSAL DESC;

-- Q-50. Write an SQL query to fetch the names of workers who earn the highest salary.
SELECT FIRST_NAME, SALARY FROM WORKER WHERE SALARY = (SELECT MAX(SALARY) FROM WORKER);
```