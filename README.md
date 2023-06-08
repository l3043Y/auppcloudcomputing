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
```
SELECT gp1.* 
FROM emp gp1
INNER JOIN
  (SELECT * FROM emp WHERE emp.deptno = 10) gp2
  ON 1 = 1
WHERE gp1.deptno = 20 ANd gp1.job = gp2.job
```
![image](https://github.com/l3043Y/auppcloudcomputing/assets/20104217/5cf52c05-518f-45fd-85a7-4b04cf942665)

3. List the emps whose Sal is same as FORD or SMITH in desc order of   Sal. 
4. List the emps whose Jobs are same as MILLER or Sal is more than   ALLEN. 
5. List the emps whose Sal is > the total remuneration of the   SALESMAN. 
6. List the emps who are Senior to ‘BLAKE’ working at CHICAGO &   BOSTON. 
7. List the emps whose jobs same as ALLEN Or SMITH. 
8. List the jobs of Deptno 10 those are not found in dept 20.
9. Find the total sal given to the ‘MGR’ 
10. Find the total annual sal to distribute job wise 11. List the emps who are not working in sales dept 
12. List the emps in dept 20 whose sal is > the avg sal of deptno 10   emps. 
13. List the emps who are senior to most recently hired emp who is   working under Mgr KING 
14. Display the details of most senior employee belongs to 1981. 15. Display the number of emps for each job group by deptno wise.


