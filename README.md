# stored-procedure
CREATE DATABASE STORED1;
USE STORED1;
CREATE TABLE WORKER(Worker_id INT PRIMARY KEY,FIRST_NAME CHAR(25),LAST_NAME CHAR (25),SALARY INT(15),JOINING_DATE DATETIME,DEPARTMENT CHAR(25));
INSERT INTO WORKER VALUES(1,'NYNA','FASIL',100000,'1990-05-05-09-00-00','IT');
INSERT INTO WORKER VALUES(2,'NYHA','FASIL',200000,'1991-07-06-09-00-00','MECH');
INSERT INTO WORKER VALUES(3,'ADIL','FAIS',300000,'1990-05-05-09-00-00','IT');
INSERT INTO WORKER VALUES(4,'NAJMA','FAISAL',400000,'1990-05-05-09-00-00','IT');
INSERT INTO WORKER VALUES(5,'SHIJILA','MAAM',100000,'1990-05-05-09-00-00','IT');
INSERT INTO WORKER VALUES(6,'ALEENA','VARGHESE',500000,'1990-05-05-09-00-00','IT');

SELECT * FROM WORKER;
#write a stored procedure takes in an IN parameter for worker_id and an OUT parameter for salary
delimiter $$
CREATE PROCEDURE get_salary1(IN Worker_id1 INT)
BEGIN
SELECT SALARY FROM WORKER WHERE Worker_id=worker_id1;
end$$
delimiter ;
call get_salary1(1);

DELIMITER $$
CREATE PROCEDURE id_dept(IN WORK_ID INT)
BEGIN
UPDATE WORKER SET DEPARTMENT=WORK_ID WHERE Worker_id=WORK_ID;
END$$
DELIMITER ;
CALL id_dept(2);


delimiter $$
CREATE PROCEDURE dept_2(IN Departmnt VARCHAR(10))
BEGIN
SELECT COUNT(Worker_id) from WORKER GROUP BY DEPARTMENT;
END $$
DELIMITER ;

CALL dept_2('IT');


delimiter //
CREATE PROCEDURE P_workercount2(IN Dept varchar(30),OUT p_workrcount INT)
BEGIN
SELECT COUNT(WORKER_ID) AS counttotal FROM WORKER WHERE DEPARTMENT=Dept ;
set p_workrcount=counttotal;
END //
DELIMITER ;

set @p_workrcount=0;
call P_workercount2('IT',@p_workrcount);


delimiter $$
CREATE PROCEDURE getAvg_salary(IN Dept1 varchar(10),OUT Avg_salary decimal(10,2))
begin
select avg(salary) as avgsal from worker where DEPARTMENT=Dept1;
set avg_salary=avgsal;
end $$
delimiter ;

set @avg_salary=0;
call getavg_salary('IT',@avg_salary);
