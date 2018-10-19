

- 查询一
```SQL
SELECT d.department_name，count(e.job_id)as "部门总人数"，
avg(e.salary)as "平均工资"
from hr.departments d，hr.employees e
where d.department_id = e.department_id
and d.department_name in ('IT'，'Sales')
GROUP BY department_name;
```
查询结果
![image](https://github.com/suerlll/oracle/blob/master/tup/cx1.png)
优化建议
代码通过查询部门名得到部门ID，最终决定部门人员，获得
- 查询二
```SQL
SELECT d.department_name，count(e.job_id)as "部门总人数"，
avg(e.salary)as "平均工资"
FROM hr.departments d，hr.employees e
WHERE d.department_id = e.department_id
GROUP BY department_name
在（'IT'，'销售'）中使用d.department_name;
```
查询结果
![image](https://github.com/suerlll/oracle/blob/master/tup/cx2.png)
优化建议
1

