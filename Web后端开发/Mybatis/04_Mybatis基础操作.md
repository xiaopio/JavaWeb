# 需求说明

根据系统页面原型，完成员工页面功能的开发

## 删除操作

```java
// 根据ID删除员工
// #{}占位符
@Delete("delete from emp where id = #{id}")
public void delete(Integer id);
```

> [!NOTE]
>
> 如果mapper接口方法形参只有一个普通类型的参数，#{...}里面的属性名可以随便写，如：#{id}、#{value}。

```
预编译SQL
==>  Preparing: delete from emp where id = ?
// 占位符的值为16
==> Parameters: 16(Integer)
// 影响了一行
<==    Updates: 1
```

## **预编译SQL**

```
优势：
	性能更高
	更安全（防止SQL注入）
```

```sql
-- 正常查询
select count(*) from emp where username = 'jinyong' and password = '123456';
-- sql注入
-- 用户名随便输入，密码只需要填写：' or '1'='1
select count(*) from emp where username = 'jdhksjhdkls' and password = '' or '1'='1';
```

> [!NOTE]
>
> 参数占位符
>
> - #{ ... }
>   - 执行SQL时，会将#{ ... }替换为？，生成预编译SQL，会自动设置参数值
>   - 使用时机：参数传递，都是用#{ ... }
> - ${ ... }
>   - 拼接SQL。将参数直接拼接到SQL语句中，存在SQL注入问题。
>   - 使用时机：如果对表名、列表进行动态设置时使用。

## 增加操作

```java
// 新增员工

@Insert("insert into emp (username, name, gender, image, job, entrydate, dept_id, create_time, update_time)"  + "values (#{username},#{name},#{gender},#{image},#{job},#{entrydate},#{deptId},#{createTime},#{updateTime})")

public void insert(Emp emp);
```

## 新增（主键返回）

描述：在数据添加成功后，需要获取插入数据库数据的主键。

如：添加套餐数据时，还需要维护套餐菜品关系数据。

**实现**

```java
// 自动将生成的主键值，赋值给emp对象的id属性
@Options(keyProperty = "id", useGenerated = true)
@Insert("insert into emp (username, name, gender, image, job, entrydate, dept_id, create_time, update_time)"  + "values (#{username},#{name},#{gender},#{image},#{job},#{entrydate},#{deptId},#{createTime},#{updateTime})")

public void insert(Emp emp);
```

## 更新操作

```sql
// 根据主键修改员工信息
    @Update("update emp set username = #{username},name = #{name},gender = #{gender},image = #{image}," +
            "job = #{job},entrydate = #{entrydate},dept_id = #{deptId},update_time = #{updateTime} where id = #{id}")
    public void update(Emp emp);
```

## 查询操作

```java
// 根据ID查询员工信息
@Select("select * from emp where id = #{id}")
public Emp getById(Integer id);
```

```java
Emp(id=19, username=Tom2, password=123456, name=汤姆2, gender=1, image=1.jpg, job=1, entrydate=2000-01-01, deptId=null, createTime=null, updateTime=null)
```

## 数据封装

> [!NOTE]
>
> - 实体类属性名 和 数据库表查询返回的字段名一致，mybatis会自动封装。
>
> - 如果实体类属性名 和 数据库表查询返回的字段名不一致，不能自动封装。

```java
// 方案一：给字段起别名，让别名与实体属性值一致

@Select("select id, username, password, name, gender, image, job, entrydate, dept_id deptId, create_time createTime, update_time updateTime from emp where id = #{id}")
public Emp getById(Integer id);
```

```java
// 方案二：通过@Results，@Result注解手动映射封装
@Results({
        @Result(column = "dept_id", property = "deptId"),
        @Result(column = "create_time", property = "createTime"),
        @Result(column = "update_time", property = "updateTime"),
})
@Select("select * from emp where id = #{id}")
public Emp getById(Integer id);
```

```
// 方案三：开启mybatis的驼峰命名自动映射开关 --  a_cloumn -----> aCloumn
```

```properties
#开启mybatis的驼峰命名自动映射开关
mybatis.configuration.map-underscore-to-camel-case=true
```

## 查询（条件查询）

```java
// 条件查询
@Select("select * from emp where name like '%${name}%' and gender = #{gender}" +
        " and entrydate between #{begin} and #{end} order by update_time desc")
public List<Emp> list(String name, Short gender, LocalDate begin, LocalDate end);
```

```sql
-- 条件查询
select * from emp where name like '%张%' and gender = 1 and entrydate between '2000-01-01' and '2022-01-01'order by update_time desc;

-- concat 字符串拼接函数
select concat('hello',' mysql',' world');
select * from emp where name like concat('%','张','%') and gender = 1 and entrydate between '2000-01-01' and '2022-01-01'order by update_time desc;
```

**改造${ ... }，防止sql注入风险**

```java
// 条件查询
@Select("select * from emp where name like concat('%',#{name},'%') and gender = #{gender}" +
        " and entrydate between #{begin} and #{end} order by update_time desc")
public List<Emp> list(String name, Short gender, LocalDate begin, LocalDate end);
```

**预编译SQL**

```sql
select * from emp where name like concat('%',?,'%') and gender = ? and entrydate between ? and ? order by update_time desc
```

