# 查询&修改&删除

```sql
-- DDL：查询表结构
-- 查看：当前数据库下的表
SHOW TABLES;

-- 查看：指定的表结构
DESC tb_emp;

-- 查看：数据库的建表语句
SHOW CREATE TABLE tb_emp;

-- DDL：修改表结构
-- 修改：为表 tb_emp 添加字段 qq varchar(11)
ALTER TABLE tb_emp ADD qq VARCHAR(11) COMMENT 'QQ';

-- 修改：修改 tb_emp 字段类型 qq varchar(13) comment 'QQ'
ALTER TABLE tb_emp MODIFY qq VARCHAR(13) COMMENT 'QQ';

-- 修改：修改 tb_emp 字段名 qq 为 qq_num varchar(13)
ALTER TABLE tb_emp CHANGE qq qq_num VARCHAR(13) COMMENT 'QQ';

-- 修改：删除 tb_emp 的 qq_num 字段
ALTER TABLE tb_emp DROP COLUMN qq_num;

-- 修改：将 tb_emp 表名修改为 emp
RENAME TABLE tb_emp TO emp;

-- DDL：删除表结构
-- 删除：删除 tb_emp 表
DROP TABLE IF EXISTS tb_emp;
```

