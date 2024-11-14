# Maven

一款用于管理和构建Java项目的工具

## 作用

依赖管理：方便快捷管理项目中的依赖资源（jar包），避免版本冲突问题

统一项目结构：提供标准、统一的项目结构

项目构建：标准跨平台的自动化项目构建方式

## IDEA集成Maven

<img src="D:\admin\Pictures\Snipaste\快捷保存\IDEA集成Maven1.png" alt="IDEA集成Maven1" style="zoom:60%;" />

<img src="D:\admin\Pictures\Snipaste\快捷保存\IDEA集成Maven2.png" alt="IDEA集成Maven2" style="zoom:60%;" />

<img src="D:\admin\Pictures\Snipaste\快捷保存\IDEA集成Maven3.png" alt="IDEA集成Maven3" style="zoom:60%;" />

## 依赖配置

## 依赖传递

```java
<dependencies>
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>3.8.1</version>
        <scope>test</scope>
    </dependency>
    <dependency>
        <groupId>ch.qos.logback</groupId>
        <artifactId>logback-classic</artifactId>
        <version>1.5.6</version>
    </dependency>
    <dependency>
        <groupId>com.haust</groupId>
        <artifactId>maven-project01</artifactId>
        <version>1.0-SNAPSHOT</version>
        <!--排除依赖-->
        <exclusions>
            <exclusion>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            </exclusion>
        </exclusions>
    </dependency>
</dependencies>
```

![maven-project – pom.xml (maven-project)_2024-11-09_17-20-03](D:\admin\Pictures\Snipaste\快捷保存\maven-project – pom.xml (maven-project)_2024-11-09_17-20-03.png)

## 依赖范围

scope标签内

**compile**（默认）:主程序、测试程序、打包（运行）

**test**：测试程序

**provided**：主程序、测试程序

**runtime**：测试程序、打包（运行）

## 生命周期

Maven的生命周期就是为了对所有的maven项目构建过程进行抽象和统一

Maven中有3套**相互独立**的生命周期

**clean**：清理工作

**default**：核心工作，如：编译、测试、打包、安装、部署等。

**site**：生成报告、发布站点等



clean：清理

compile：编译

test：测试

package：打包

install：安装



