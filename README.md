# SQL AND DBMS 2023
--- 
 
## Day 1 

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
## DAY 2


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

