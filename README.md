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


3. sdf

