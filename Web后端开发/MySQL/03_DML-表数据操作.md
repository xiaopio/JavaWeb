# DML表数据操作

## 添加数据insert

```sql
-- DML:数据库操作语言
-- DML：插入数据 - insert
-- 1.为 tb_emp 表的 username，name，gender 字段插入值
INSERT INTO tb_emp ( username, `name`, gender, create_time, update_time )
VALUES
  ( 'zhangwuji', '张无忌', 1, NOW( ), NOW( ) );

-- 2.为 tb_emp 表的 所有字段插入值
INSERT INTO tb_emp ( id, username, `password`, `name`, gender, image, job, entrydate, create_time, update_time )
VALUES
  ( NULL, 'yangmi', '123', '杨幂', '2', '1.jpg', '2', '2010-01-01', NOW( ), NOW( ) );

-- 3.批量操作 为 tb_emp 表的 username，name，gender 字段插入数据
INSERT INTO tb_emp ( username, `name`, gender, create_time, update_time )
VALUES
  ( 'zhaoliying', '赵丽颖', '2', NOW( ), NOW( ) ),
  ( 'huge', '胡歌', '1', NOW( ), NOW( ) ),
  ( 'liushishi', '刘诗诗', '2', NOW( ), NOW( ) ),
  ( 'linzicong', '林子聪', '1', NOW( ), NOW( ) );

```

## 修改数据update

```sql
-- DML：更新数据 - update
-- 1.将 tb_emp 表的ID为1员工 姓名name 字段更新为 '张三'
UPDATE tb_emp 
SET username = 'zhangsan',
update_time = NOW( ) 
WHERE
  id = 1;
  
-- 2.将 tb_emp 表的所有员工的入职日期更新为 '2010-01-01'
UPDATE tb_emp 
SET entrydate = '2010-01-01',
update_time = NOW( )
```

## 删除数据delete

```sql
-- DML：删除数据 - delete
-- 1.删除 tb_emp 表中 ID为1的员工
DELETE 
FROM
  tb_emp 
WHERE
  id = 1;

-- 2.删除 tb_emp 表中的所有员工
DELETE 
FROM
  tb_emp;
```

