# auppcloudcomputing
1. List the emps who are senior to their own MGRs
```sql
SELECT * 
FROM emp ep 
WHERE ep.hiredate < (
  SELECT ep2.hiredate
  FROM emp ep2
  WHERE ep2.empno = ep.mgr
);
```
![image](https://github.com/l3043Y/auppcloudcomputing/assets/20104217/8076f76d-2c3b-4543-bccc-d276f1faf76d)

2. List the emps of deptno 20 whose jobs are same as deptno 10
```sql
SELECT gp1.* 
FROM emp gp1
INNER JOIN
  (SELECT * FROM emp WHERE emp.deptno = 10) gp2
  ON 1 = 1
WHERE gp1.deptno = 20 ANd gp1.job = gp2.job
```
![image](https://github.com/l3043Y/auppcloudcomputing/assets/20104217/5cf52c05-518f-45fd-85a7-4b04cf942665)

3. List the emps whose Sal is same as FORD or SMITH in desc order of   Sal. 
```sql
SELECT * 
FROM emp gp1
WHERE gp1.sal IN (
  SELECT gp2.sal
  FROM emp gp2
  WHERE gp2.ename IN ('FORD', 'SMITH')
)
ORDER BY gp1.sal DESC
```
![image](https://github.com/l3043Y/auppcloudcomputing/assets/20104217/b324e53d-9b58-46e5-b8b0-9bae57bea683)

4. List the emps whose Jobs are same as MILLER or Sal is more than ALLEN. 
```sql
SELECT * 
FROM emp gp1
WHERE 
  gp1.job IN (
    SELECT gp2.job
    FROM emp gp2
    WHERE gp2.ename IN ('MILLER')
  )
  OR gp1.sal > (
    SELECT gp3.sal
    FROM emp gp3
    WHERE gp3.ename = 'ALLEN'
  );
```
![image](https://github.com/l3043Y/auppcloudcomputing/assets/20104217/5b5b20e0-68ff-477e-9576-a02b8d1423db)

5. List the emps whose Sal is > the total remuneration of the   SALESMAN. ???
```sql
SELECT * 
FROM emp gp1
WHERE gp1.sal > (
  SELECT SUM(gp2.sal)
  FROM emp gp2
  WHERE gp2.job = 'SALESMAN'
  );
```
![image](https://github.com/l3043Y/auppcloudcomputing/assets/20104217/424d92aa-5fe3-4038-9157-44df4c1810dd)

6. List the emps who are Senior to ‘BLAKE’ working at CHICAGO &   BOSTON. 
```sql
SELECT emp1.* 
FROM emp emp1
	INNER JOIN dept on dept.deptno = emp1.deptno
WHERE 
  emp1.hiredate < (
    SELECT emp2.hiredate
    FROM emp emp2
    WHERe emp2.ename = 'BLAKE'
  )
  AND dept.loc IN ('CHICAGO', 'BOSTON')
;
```
![image](https://github.com/l3043Y/auppcloudcomputing/assets/20104217/021d8185-6e4e-402d-b038-dfc37ca94182)
7. List the emps whose jobs same as ALLEN Or SMITH. 
```sql
SELECT emp1.* 
FROM emp emp1
WHERE emp1.job IN (
  SELECT emp2.job
  FROm emp emp2
  WHERE emp2.ename IN ('ALLEN', 'SMITH')
);
```
![image](https://github.com/l3043Y/auppcloudcomputing/assets/20104217/13069815-2c18-4c1e-b27a-a3738a2c3ace)
8. List the jobs of Deptno 10 those are not found in dept 20.
```sql
WITH jobs(title, deptno) as (
  SELECT DISTINCT emp1.job AS title, dept.deptno as deptno
  FROM emp emp1
  INNER JOIN dept on emp1.deptno = dept.deptno
)
SELECT DISTINCT j1.title
FROM jobs j1
WHERE j1.deptno = 10 and j1.title NOT IN (
  SELECT j2.title
  FROM jobs j2
  WHERE j2.deptno = 20
);
```
![image](https://github.com/l3043Y/auppcloudcomputing/assets/20104217/e4b55de1-6530-451f-8f37-601a977885f7)
9. Find the total sal given to the ‘MGR’ 
```sql
SELECT SUM(emp1.sal)
FROM emp emp1
WHERe emp1.job = "MANAGER"
```
![image](https://github.com/l3043Y/auppcloudcomputing/assets/20104217/969bb5ae-9c12-451e-9cc4-37c0d6ca9a3a)
10. Find the total annual sal to distribute job wise ??/
```sql
SELECT ep.job, SUM(ep.sal)
FROM emp ep
GROUP by ep.job
```
![image](https://github.com/l3043Y/auppcloudcomputing/assets/20104217/371a603c-f823-45a9-88e9-064a6e079f7f)

11. List the emps who are not working in sales dept 
```sql
WITH tmp as (
  SELECT emp1.*, dept.dname
  FROM emp emp1
  INNER JOIN dept on emp1.deptno = dept.deptno
)
SELECT * FROM tmp WHERE tmp.dname IS NOT "SALES"
```
![image](https://github.com/l3043Y/auppcloudcomputing/assets/20104217/444fd7ad-9a85-4ff5-b975-732004dab7a0)

12. List the emps in dept 20 whose sal is > the avg sal of deptno 10   emps. 
```sql
SELECT *
FROM emp ep1
WHERE 
	ep1.sal > (
    SELECT AVG(ep2.sal)
    FROM emp ep2
    WHERE ep2.deptno = 10
    )
    AND ep1.deptno = 20
```
![image](https://github.com/l3043Y/auppcloudcomputing/assets/20104217/6b1e0e03-9c8b-4934-950d-c61d7ad236f4)

13. List the emps who are senior to most recently hired emp who is   working under Mgr KING 
```sql
SELECT * 
FROM emp ep
where ep.hiredate < (
  SELECT ep1.hiredate
  FROM emp ep1
  WHERE ep1.mgr = (
  	SELECT ep2.empno
    FROM emp ep2
    WHERE ep2.ename = 'KING'
  )
  ORDER BY hiredate DESC
  LIMIT 1
);
```
![image](https://github.com/l3043Y/auppcloudcomputing/assets/20104217/cd6d5711-0a83-439f-b93e-83da2990d877)
14. Display the details of most senior employee belongs to 1981. 
```sql
SELECT *
FROM emp ep
WHERE strftime("%Y",ep.hiredate) = '1981'
ORDEr BY ep.hiredate ASC
LIMIT 1
```
![image](https://github.com/l3043Y/auppcloudcomputing/assets/20104217/ed9247da-6599-4546-8a7b-58e21f82ee50)
15. Display the number of emps for each job group by deptno wise.
```sql
SELECT ep.deptno, COUNT(*) as cnt
FROM emp ep
GROUP by ep.deptno
```
![image](https://github.com/l3043Y/auppcloudcomputing/assets/20104217/ac5f25e1-24c1-4d1d-ab44-0202338cffcc)


