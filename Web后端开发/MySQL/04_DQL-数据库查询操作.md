# DQL

**Data Query Language（数据查询语言）**

select 字段列表（基本查询**↓**）

from 表名列表

where 条件列表（条件查询）

group by 分组字段列表（分组查询↓）

having 分组后条件列表

order by 排序字段列表（分页查询↓）

limit 分页参数

## 基本查询(select...from...)

```sql
-- DQL：基本查询
-- 1.查询指定字段 name，entrydate 并返回
SELECT
  `name`,
  entrydate 
FROM
  tb_emp;

-- 2.查询返回所有字段
-- 推荐
SELECT
  id,
  username,
  password,
  name,
  gender,
  image,
  job,
  entrydate,
  create_time,
  update_time 
FROM
  tb_emp;
  
-- 不推荐（不直观，性能低）
SELECT
  * 
FROM
  tb_emp;
  
-- 3.查询所有员工的 name，entrydate，并起别名（姓名、入职日期）
SELECT name AS
  姓名,
  entrydate AS 入职日期 
FROM
  tb_emp;
  
-- 注意：别名中有空格要用''包裹起来，表示这是一个整体
SELECT name
  '姓名',
  entrydate '入职日期' 
FROM
  tb_emp;
  
-- 4.查询已有的员工关联了哪几种职位（distinct不要重复）
SELECT DISTINCT
  job 
FROM
  tb_emp;
```

## 条件查询(where...)

| 比较运算符         | 功能                                       |
| ------------------ | ------------------------------------------ |
| >                  | 大于                                       |
| >=                 | 大于等于                                   |
| <                  | 小于                                       |
| <=                 | 小于等于                                   |
| =                  | 等于                                       |
| <> 或 !=           | 不等于                                     |
| between... and ... | 在某个范围之内（含最小、最大值）           |
| in( . . . )        | 在 in 之后的列表中的值，多选一             |
| like    占位符     | 模糊匹配（_匹配单个字符，%匹配任意个字符） |
| is null            | 是null                                     |

| 逻辑运算符 | 功能                         |
| ---------- | ---------------------------- |
| and 或 &&  | 并且（多个条件同时成立）     |
| or 或\|\|  | 或者（）多个条件任意一个成立 |
| not 或 !   | 非，不是                     |

```sql
-- DQL：条件查询
-- 1.查询 姓名 为 杨逍 的员工
SELECT * FROM tb_emp WHERE NAME = '杨逍';

-- 2.查询 id 小于 5 的员工信息
SELECT * FROM tb_emp WHERE id <= 5;

-- 3.查询 没有分配职位 的员工
SELECT * FROM tb_emp WHERE job IS NULL;

-- 4.查询 有职位 的员工
SELECT * FROM tb_emp WHERE job IS NOT NULL;

-- 5.查询 密码不等于 '123456' 的员工信息
SELECT * FROM tb_emp WHERE password != '123456';
SELECT * FROM tb_emp WHERE password <> '123456';

-- 6.查询 入职时间 在 '2000-01-01'(包含) 到 '2010-01-01'(包含) 之间的员工信息
SELECT * FROM tb_emp WHERE entrydate >= '2000-01-01' AND entrydate <= '2010-01-01'
SELECT * FROM tb_emp WHERE entrydate >= '2000-01-01' && entrydate <= '2010-01-01'
SELECT * FROM tb_emp WHERE entrydate BETWEEN '2000-01-01' AND '2010-01-01'

-- 7.查询 入职时间 在 '2000-01-01'(包含) 到 '2010-01-01'(包含) 之间 且 性别为女 的员工信息
SELECT * FROM tb_emp WHERE entrydate BETWEEN '2000-01-01' AND '2010-01-01' AND gender = 2;

-- 8.查询 职位是 2（讲师），3（学工主管），4（教研主管）的员工信息
SELECT * FROM tb_emp WHERE job = 2 OR job = 3 OR job = 4;
SELECT * FROM tb_emp WHERE job = 2 || job = 3 || job = 4;
SELECT * FROM tb_emp WHERE job IN (2, 3, 4);

-- 9.查询 姓名 为 两个字 的员工
SELECT * FROM tb_emp WHERE `name` LIKE '__';

-- 10.查询 姓氏 为 '张' 的员工
SELECT * FROM tb_emp WHERE `name` LIKE '张%';
```

## 分组查询(group by...having...)

**聚合函数**

介绍：将一列数据作为一个整体，进行纵向计算

语法：select 聚合函数（字段列表） from 表名

| 函数  | 功能     |
| ----- | -------- |
| count | 统计数量 |
| max   | 最大值   |
| min   | 最小值   |
| avg   | 平均值   |
| sum   | 求和     |

```sql
-- 聚合函数
-- 1. 统计该企业员工数量 -- count --29人

-- A.count(字段)
-- 29
SELECT COUNT(id) FROM tb_emp; -- 29
SELECT COUNT(`name`) FROM tb_emp; -- 29
-- 聚合函数 不对null值进行计算
SELECT COUNT(job) FROM tb_emp; -- 28

-- B.count(常量)
SELECT COUNT(0) FROM tb_emp; -- 29

-- C.count(*) -- 推荐
SELECT COUNT(*) FROM tb_emp; -- 29

-- 2.统计该企业 最早入职 的员工 -- min
SELECT MIN(entrydate) FROM tb_emp;

-- 3.统计该企业 最迟入职 的员工 -- max
SELECT MAX(entrydate) FROM tb_emp;

-- 4.统计该企业员工 ID 的平均值 -- avg
SELECT AVG(id) FROM tb_emp;

-- 5.统计该企业员工 ID 之和 -- sum
SELECT SUM(id) FROM tb_emp;
```

> [!WARNING]
>
> null值不参与所有聚合函数的运算
>
> 统计数量可以使用：count( * )、count(字段)、count(常量)，推荐使用count( * )

```sql
-- 分组
-- 1.根据性别分组，统计男性和女性员工的数量 - count(*)
SELECT gender,COUNT(*) FROM tb_emp GROUP BY gender

-- 2.先查询入职时间在 '2015-01-01' (包含) 以前的员工，并对结果根据职位进行分组，获取员工数量大于等于2的职位
SELECT job,COUNT(*) FROM tb_emp WHERE entrydate <= '2015-01-01' GROUP BY job HAVING COUNT(*) >= 2; 
```

## 排序查询(order by...)

| 排序方式            |
| ------------------- |
| ASC：升序（默认值） |
| DESC：降序          |

> [!NOTE]
>
> 如果是多字段排序，当第一个字段值相同时，才会根据第二个字段进行排序



```sql
-- 排序查询
-- 1.根据入职时间，对员工进行升序排序 -- ASC
SELECT * FROM tb_emp ORDER BY entrydate ASC;

-- 2.根据入职时间，对员工进行降序排序 -- DESC
SELECT * FROM tb_emp ORDER BY entrydate DESC;

-- 3.根据 入职时间 对公司员工进行 升序排序 ，入职时间相同，再按照 更新时间 进行 降序排序
SELECT * FROM tb_emp ORDER BY entrydate ASC ,update_time DESC;
```

## 分页查询(limit...)

```sql
-- 分页查询
-- select 字段列表 from 表名 limit 起始索引,查询记录数;
-- 1.从 起始索引 0 开始查询员工数据，每页展示5条记录
SELECT * FROM tb_emp LIMIT 0, 5;

-- 2.查询 第1页 员工数据，每页展示5条数据
SELECT * FROM tb_emp LIMIT 0, 5;

-- 3.查询 第2页 员工数据，每页展示5条数据
SELECT * FROM tb_emp LIMIT 5, 5;

-- 4.查询 第3页 员工数据，每页展示5条数据
SELECT * FROM tb_emp LIMIT 10, 5;

-- 起始索引 = （页码 - 1）*（每页展示的记录数）
```

> [!NOTE]
>
> 1. 起始索引从 0 开始，起始索引 = （页码 - 1）*（每页展示的记录数）。
> 2. 分页查询是数据库的方言，不同的数据库有不同的实现，MySQL中是LIMIT。
> 3. 如果查询的是第一页数据，起始索引可以省略，直接简写为 limit 10。

## 案例

### 1-1

根据条件，查询第一页数据，每页展示10条记录

输入条件

​	姓名：张

​	性别：男

​	入职日期：2000-01-01	2015-12-31

要求结果按照最后更新时间进行倒叙排序

```sql
SELECT
  * 
FROM
  tb_emp 
WHERE
  `name` LIKE '张%' 
  AND gender = 1 
  AND entrydate BETWEEN '2000-01-01' 
  AND '2015-12-31' 
ORDER BY
  update_time DESC 
LIMIT 
  0, 10;
```

### 2-1

根据需求完成员工信息的统计

员工性别的统计

```sql
-- if(条件表达式, true取值, false取值)
SELECT
IF
  ( gender = 1, '男性员工', '女性员工' ) 性别,
  COUNT( * ) 
FROM
  tb_emp 
GROUP BY
  gender;
```

员工职位统计

```sql
-- case 表达式 when 值1 then 结果1 when 值2 then 结果2 ... else ... end
SELECT
  ( CASE job WHEN 1 THEN '班主任' WHEN 2 THEN '讲师' WHEN 3 THEN '学工主管' WHEN 4 THEN '教研主管' ELSE '未分配职位' END ) 职位,
  COUNT( * ) 
FROM
  tb_emp 
GROUP BY
  job;
```

