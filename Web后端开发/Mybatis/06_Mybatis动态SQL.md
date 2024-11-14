# 动态SQL

随着用户的输入或外部条件的变化而变化的SQL语句，称之为**动态SQL**

## < if >

< if > ：用于判断条件是否成立。使用test属性进行条件判断，如果结果为true，则拼接SQL。

```java
<if test="name != null">
    	name like concat('%',#{name},'%')
</if>
```

```xml
<select id="list" resultType="com.haust.pojo.Emp">
    select *
    from emp
    <where>
        <if test="name != null">
            name like concat('%', #{name}, '%')
        </if>
        <if test="gender != null">
            and gender = #{gender}
        </if>
        <if test="begin != null and end != null">
            and entrydate between #{begin} and #{end}
        </if>
    </where>
    order by update_time desc
</select>
```

## < where >

< where >：where 元素只会在子元素有内容的情况下才插入where子句。而且会自动去除子句开头多余的 AND 或 OR



案例

完善更新员工的功能，修改为动态的更新员工的信息

需求：动态更新员工信息，如果更新时有值传递，则更新；如果更新时没有值传递，则不更新。

## < set >

< set >：动态地在行首插入SET关键字，并会删除额外的逗号。（用在update语句中）

```xml
<update id="update">
    update emp
    <set>
        <if test="username != null">
            username = #{username},
        </if>
        <if test="name != null">
            name = #{name},
        </if>
        <if test="gender != null">
            gender = #{gender},
        </if>
        <if test="image != null">
            image = #{image},
        </if>
        <if test="job != null">
            job = #{job},
        </if>
        <if test="entrydate != null">
            entrydate = #{entrydate},
        </if>
        <if test="deptId != null">
            dept_id = #{deptId},
        </if>
        <if test="updateTime != null">
            update_time = #{updateTime}
        </if>
    </set>
    where id = #{id}
</update>
```

## < foreach >

```xml
<!--批量删除员工-->
<!--
    collection：遍历的集合
    item：遍历出来的元素
    separator：分隔符
    open：遍历开始前拼接的SQL片段
    close：遍历结束后拼接的SQL片段
-->
<delete id="deleteByIds">
    delete from emp where id in
    <foreach collection="ids" item="id" separator="," open="(" close=")">
        #{id}
    </foreach>
</delete>
```

## < sql > < include >

 

< sql >：定义可重用的SQL片段

< include >：通过属性refid，指定包含的sql片段

```xml
    <sql id="commonSelect">
        select id, username, password, name, gender, image, job, entrydate, dept_id, create_time， update_time
        from emp
    </sql>
```

```xml
<!--根据员工姓名、性别、入职日期动态查询-->
<select id="list" resultType="com.haust.pojo.Emp">
    <include refid="commonSelect"/>
    <where>
        <if test="name != null">
            name like concat('%', #{name}, '%')
        </if>
        <if test="gender != null">
            and gender = #{gender}
        </if>
        <if test="begin != null and end != null">
            and entrydate between #{begin} and #{end}
        </if>
    </where>
    order by update_time desc
</select>
```

