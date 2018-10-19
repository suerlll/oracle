
- 查询一
```SQL
SELECT d.department_name，count(e.job_id)as "部门总人数"，
avg(e.salary)as "平均工资"
from hr.departments d，hr.employees e
where d.department_id = e.department_id
and d.department_name in ('IT'，'Sales')
GROUP BY department_name;
```
查询结果：
![](https://github.com/suerlll/oracle/blob/master/tup/cx1.png)
分析：
代码通过查询部门名得到部门ID，最终决定部门人员，获得人数和工资，最后按照部门名输出。应该精准定位至人员，是查询更加准确。
- 查询二
```SQL
SELECT d.department_name，count(e.job_id)as "部门总人数"，
avg(e.salary)as "平均工资"
FROM hr.departments d，hr.employees e
WHERE d.department_id = e.department_id
GROUP BY department_name
在（'IT'，'销售'）中使用d.department_name;
```
查询结果：
！[]（https://github.com/suerlll/oracle/blob/master/tup/cx2.png)
分析：
代码通过查询部门人员来得到数据。准确的定位与输出。较查询一更加优秀。
查询一与查询二相较而言，查询二更加的好。
- 查询三

