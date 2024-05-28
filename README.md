# SQL AND DBMS 2023
--- 
 
## Day 1 ✅

### Data types in SQL
```
- int
- varchar2
- Number
- Date   DD-MMM-YY (03-AUG-18)  DD-MMM-YYY (03-AUG-2024)
```

### Start Connection
```
connect
enter username
enter password
```
### Creating Table
```
CREATE TABLE STUDENT
(
  ID VARCHAR2(3)   // PRIMARY KEY,
  NAME VARCHAR2(20),
  CITY VARCHAR(10),
  SALARY NUMBER(10),
  DOB DATE,
  PRIMARY KEY(ID)
  // PRIMARY KEY(ID,NAME) MORE THAN ONE ATTRIBUTES ARE PRIMARY KEY => COMPOSIT KEY 
);
```

### Describe Tabel
` DESC TABLE-NAME `

### Drop Table 
` DROP TABLE Table-Name` it will delete TABLE totaly

### Insert value & Display Table
```
INSERT INTO STUDENT VALUES('E01','SRIJIT','PUNE',52000,'08-AUG-2002');

SELECT * FORM EMPLOYEE WHERE AGE=69;

```
### Delete Column and Rows
```
DELETE FROM STUDENT;                        //will delete the all rows of the table

DELETE FROM STUDENT WHERE NAME='SRIJIT'; // Tthis only delete that only filtered row
```

### UpdaTE Table
```
UPDATE STUDENT SET NAME='KAMALIKA' WHERE ID='E01'
```

### ORDER BY
```
ORDER BY SALARY DESC

It will sort by default in Assecnding order
`DESC` eill srot in decending order
```

---
## DAY 2 ✅


### ALTER 

- Add new column
 ```
 ALTER TABLE STUDENT ADD REGNO NUMBER(5);
 ```

- Modify
 ```
 ALTER TABLE STUDENT MODIFT REGNO NUMBER(10);   //Only you can make the number value increase
 ```

- Add Primary Key
 ```
 ALTER TABLE STUDENT ADD PRIMARY KEY(ID);
 ```

### BETWEEN

 ```
 SELECT * FROM STUDENT WHERE SALARY BETWEEN 5000 AND 70000;

 ```
 
 ### IN & NOT IN
 ```
 SELECT * FROM STUDENT WHERE CITY IN('KOLKATA','PUNE');

 SELECT * FROM STUDENT WHERE CITY NOT IN('KOLKATA','PUNE');
 ```

 ### LIKE & NOT LIKE
 ```
 Show me thE name of the employee start with 'A'


  SELECT * FROM STUDENT WHERE NAME LIKE 'A%'   //START WITH A END WITH ANYTHING
  SELECT * FROM STUDENT WHERE NAME LIKE '_A%'   //SECOND LETTER IS A END WITH ANYTHING
  SELECT * FROM STUDENT WHERE NAME LIKE '%A%'   //ANYWHERE EXCLUDING LAST AND FIRST POSITION
  SELECT * FROM STUDENT WHERE NAME LIKE '%A%' AND NOT LIKE 'A%'  // CONTAIN A BUT NOT START WITH A
 ```

 ### ALICE 
  ` SELECT (NAME|| ' '|| SALARY) "NAME" FROM STUDENT;  // YOU CAN WRITE AS OR NOT `

### AGGREGET FUNCTION
 - MAX
 - MIN
 - SUM
 - AVG
 - COUNT
 - SQRT

### DATE OF BIRTH
 ```
 SELECT TRUNC(TRUNC(SYSDATE-DOB)/365) "AGE" FROM STUDENT;
 SELECT MAX(TRUNC(TRUNC(SYSDATE-DOB)/365)) "MAXAGE" FROM STUDENT
 ```

---

## DAY 3 ✅

`Aggregate function only can use after Select and Having clause`

### Find Max & Min Salary 
```
SELECT * FROM EMPLOYEE WHERE SALARY = (SELECT MAX(SALARY) FROM EMPLOYEE);             //1st Max


SELECT MAX(SALARY) FROM EMPLOYEE WHERE SALARY < (SELECT MAX(SALARY) FROM EMPLOYEE);   
SELECT * FROM EMPLOYEE WHERE SALARY = (SELECT MAX(SALARY) FROM EMPLOYEE WHERE SALARY < (SELECT MAX(SALARY) FROM EMPLOYEE));        ///2nd Max

```

### Oldest Employee

 ```
 SELECT * FROM STUDENT WHERE TRUNC((SYSDATE-DOB)/365) =(SELECT MAX(TRUNC((SYSDATE-DOB)/365)) Age  FROM STUDENT);

 ```

  - USE ` Distinct ` to remove duplicate

### Check Constraint 

```
CREATE TABLE STUDENT
(
  ID VARCHAR2(3) CHECK (ID LIKE 'E%'),                      //check is the eid start with E
  NAME VARCHAR2(20) NOT NULL,
  CITY VARCHAR(10) CHECK( CITY IN('KOLKATA','PUNE' ,'DELHI')),
  SALARY NUMBER(10) CHECK (SALARY >=5000),
  DOB DATE,
  PRIMARY KEY(ID)
);

```
### Foreign Keyword 

---

## Day 4 ✅
Required Table 👇👇
![Screenshot 2024-05-07 213845](https://github.com/yourSrijit/DBMS-Oracle-SQL/assets/91645620/c3629f22-3b26-470f-af65-fbd316d991dc)

`Joinning` 

```
SELECT E.* FROM EMPLOYEE E,WORK W ,DEP D WHERE E.ID = W.DID AND D.DID = W.DID WHERE NAME="AJAY"; 

SELECT NAME FROM EMPLOYEE WHERE ID IN(SELECT ID FROM WORK WHERE DID IN (SELECT DID FROM DEP WHERE DNAME="HR"));

```

### GROUP BY  [EACH, EVERY ,ALL]
 
- `GROUP BY` IS USED AFTRE WHERE KEYWORD
- `ORDER BY` IS USED AFTER GROUP BY KEYWORD
- THE FIELD IS USED AFTER GROUP BY THIS IS MENDATORY THING `IT HAS TO BE AFTER SELECT KEYWORD [Exception : Aggregate Function]`
- AGGREGATE FUN ONLY USE AFTER SELECT KEYWORD AND ONLY `GROUP BY` KEYWORD

-> DISPLAY THE DEPERTMENT ID AND THE NO OF THE EMPLOYEE WORK IN THAT DEPERTMENT

```
SELECT DID,COUNT(EID) FROM WORK GROUP BY DID ORDER BY DID DESC;
``` 

### HAVING KEYWORD
->DISPLAY THE ID NO AND THE NO OF EMPLOYEE MORE THAN EQUAL TO 2  
```

SELECT DID,COUNT(ID) FROM WORK GROUP BY DID HAVING COUNT(ID)>=2;  
```



---
## Joining in Oracle SQL
 JOIN clause is used to combine data from two or more table based on related column between them.
 There have for kind of Join method in Sql
 - 1.Inner Join       -> Return Common element
 - 2.Left Join        -> Return all record from left and the matched record from right table
 - 3.Right Join       -> Return all record from right and the matched record from left table
 - 4.Full Outer Join  -> Returns all records when there is a match in either left or right table

 ---
 ```
 First Create the Table ✅✅


 CREATE TABLE EMPLOYEE (
  employee_id NUMBER,
  employee_name VARCHAR2(50),
  department_id NUMBER
);
INSERT INTO employee (employee_id, employee_name, department_id)
VALUES (1, 'John Doe', 1);

INSERT INTO employee (employee_id, employee_name, department_id)
VALUES (2, 'Jane Smith', 2);

INSERT INTO employee (employee_id, employee_name, department_id)
VALUES (3, 'Michael Johnson', 1);
--------------------------------------------------------------->

CREATE TABLE work (
  employee_id NUMBER,
  project_id NUMBER,
  hours_worked NUMBER
);
INSERT INTO work (employee_id, project_id, hours_worked)
VALUES (1, 101, 20);

INSERT INTO work (employee_id, project_id, hours_worked)
VALUES (1, 102, 15);

INSERT INTO work (employee_id, project_id, hours_worked)
VALUES (2, 101, 25);

INSERT INTO work (employee_id, project_id, hours_worked)
VALUES (3, 102, 10);

INSERT INTO work (employee_id, project_id, hours_worked)
VALUES (4, 105, 15);
INSERT INTO work (employee_id, project_id, hours_worked)
VALUES (5, 106,16);
INSERT INTO work (employee_id, project_id, hours_worked)
VALUES (6, 107, 17);

 ```

 --- 
 ### Inner Join 
 ```
 SELECT E.* FROM EMPLOYEE E INNER JOIN WORK W ON E.EMPLOYEE_ID = W.EMPLOYEE_ID;

 ```
### Left Join

```
SELECT E.* FROM EMPLOYEE E LEFT JOIN WORK W ON E.EMPLOYEE_ID = W.EMPLOYEE_ID;
```

### Right Join 
```
SELECT E.* FROM EMPLOYEE E RIGHT JOIN WORK W ON E.EMPLOYEE_ID = W.EMPLOYEE_ID;
```
### Full Join or Full Outer Join
```
SELECT E.* FROM EMPLOYEE E RIGHT JOIN WORK W ON E.EMPLOYEE_ID = W.EMPLOYEE_ID;
``` 