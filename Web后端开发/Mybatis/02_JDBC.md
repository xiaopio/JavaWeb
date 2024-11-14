## **编程方式**

- JDBC
  - JDBC 是 Java 原生的数据库访问技术，编程方式比较底层。开发人员需要手动编写大量的代码来处理数据库连接、SQL 语句的执行、结果集的处理等操作。例如，在使用 JDBC 查询数据时，需要通过`DriverManager`获取数据库连接，使用`Statement`或`PreparedStatement`来执行 SQL 语句，然后通过`ResultSet`来遍历和获取结果集中的数据，代码逻辑较为复杂。

```sql
try {
    // 加载驱动
    Class.forName("com.mysql.cj.jdbc.Driver");
    // 获取连接
    Connection connection = DriverManager.getConnection("jdbc:mysql://localhost:3306/mydb", "username", "password");
    // 创建Statement
    Statement statement = connection.createStatement();
    // 执行查询语句
    ResultSet resultSet = statement.executeQuery("SELECT * FROM users");
    while (resultSet.next()) {
        System.out.println(resultSet.getString("username"));
    }
    // 关闭资源
    resultSet.close();
    statement.close();
    connection.close();
} catch (Exception e) {
    e.printStackTrace();
}
```

- Mybatis
  - Mybatis 是一个持久层框架，它采用了一种半自动化的 SQL 映射方式。开发人员主要通过编写 XML 配置文件或使用注解来定义 SQL 语句和对象之间的映射关系。它在一定程度上简化了数据库操作，减少了代码量。例如，在 Mybatis 中，可以在 XML 文件中定义一个查询语句的映射，然后通过接口方法调用就能获取到查询结果，不需要像 JDBC 那样手动处理结果集的遍历等操作。
  - 代码示例如下：
  - 首先是定义接口：

```sql
public interface UserMapper {
    List<User> selectUsers();
}
```

- 然后是 XML 配置文件（部分内容）：

```sql
<mapper namespace="com.example.dao.UserMapper">
    <select id="selectUsers" resultMap="UserResultMap">
        SELECT * FROM users
    </select>
    <resultMap id="UserResultMap" type="com.example.entity.User">
        <id property="id" column="id"/>
        <result property="username" column="username"/>
    </resultMap>
</mapper>
```

## SQL 与代码的分离程度

- JDBC
  - SQL 语句通常是硬编码在 Java 代码中的。这使得 SQL 语句和 Java 代码紧密耦合，如果需要修改 SQL 语句，就必须修改 Java 代码，而且在复杂的 SQL 语句（如带有多个子查询、联合查询等）情况下，会使 Java 代码变得混乱和难以维护。
- Mybatis
  - Mybatis 具有很好的 SQL 与代码分离特性。SQL 语句可以写在 XML 配置文件中或者通过注解写在接口方法上，这样就可以将数据库操作的逻辑（SQL 语句）和业务逻辑（Java 代码）分开。修改 SQL 语句时，只需要在配置文件或注解中进行修改，而不需要大量改动 Java 代码，提高了代码的可维护性。

## 性能方面

- JDBC
  - 性能上，由于 JDBC 是比较底层的 API，如果合理使用`PreparedStatement`等机制，并且在代码编写上进行优化（如正确地管理数据库连接池等），可以获得较高的性能。但是，开发人员需要花费更多的精力来进行这些性能优化工作，例如手动控制数据库连接的创建和释放，不合理的操作可能导致资源浪费或者性能下降。
- Mybatis
  - Mybatis 在性能上也有不错的表现。它内部对 SQL 的执行进行了优化，并且可以方便地集成数据库连接池。同时，Mybatis 的一级缓存和二级缓存机制可以减少数据库的频繁访问，提高数据访问效率。不过，如果缓存配置不当，可能会出现数据不一致等问题。

## 可移植性和数据库兼容性

- JDBC
  - JDBC 本身是 Java 标准的数据库访问接口，理论上具有很好的可移植性和数据库兼容性。只要有相应的数据库驱动，就可以在不同的数据库之间切换。但是，由于不同数据库的 SQL 语法和特性存在差异，在实际切换数据库时，可能需要对 SQL 语句进行大量的修改。
- Mybatis
  - Mybatis 同样具有较好的可移植性和数据库兼容性。它通过 SQL 映射的方式，在一定程度上隔离了数据库之间的差异。在切换数据库时，只要修改 SQL 映射文件中的部分 SQL 语法（如果有不兼容的部分），就可以适应新的数据库。而且 Mybatis 支持多种数据库，如 MySQL、Oracle、SQL Server 等。

## 开发效率

- JDBC
  - 开发效率相对较低，因为需要编写大量的底层代码来处理数据库操作。特别是在处理复杂的数据库操作和对象关系映射时，会花费开发人员较多的时间和精力。
- Mybatis
  - Mybatis 可以显著提高开发效率。它的自动映射功能和 SQL 与代码分离的特性，使得开发人员可以更专注于业务逻辑的实现。在处理对象关系映射（如将数据库表中的列映射到 Java 对象的属性）时，Mybatis 提供了简单而有效的方式，减少了开发过程中的工作量。