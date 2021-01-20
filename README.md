# MavenStudent

#用于Maven项目的学习

#MavenDemo，MavenDemo4，MavenDemo5.三个项目用来学习了maven项目之间依赖与继承的关系

#其中有一些点：

**pom文件中jar包的管理**

1.导入jar包依赖的时候有两个原则：第一：链路最短原则，链路最短失效时，则使用第二原则：最先定义优先原则

2.依赖的范围设置<scope>

>1：provided(使用此依赖范围的Maven依赖,因为运行项目时容器提供了，就不再重复引入)
>2:runtime（编译时不生效，运行时生效）
>3：system(显示的指定本地系统路径的jar包systemPath)
>4：test(只在编译测试代码和运行测试的时候生效)
>5：import(只适用于pom文件中的依赖管理scope中)

3.排除某一个jar包

```
<exclusions>
	<exclusion>
		<groupId>com.sxh</groupId>
		<artifactId>MavenDemo</artifactId>
	</exclusion>
</exclusions>
```

4.版本管理

```
<properties>
        <MavenDemo4>1.0-SNAPSHOT</MavenDemo4>
    </properties>
    <!--jar包管理-->
    <dependencyManagement>
        <dependencies>
            <dependency>
                <groupId>com.sxh</groupId>
                <artifactId>MavenDemo</artifactId>
                <version>${MavenDemo4}</version>
                <scope>import</scope>
            </dependency>
        </dependencies>
    </dependencyManagement>
```
5.子工程引用父工程

```
 <parent>
        <groupId>com.sxhh</groupId>
        <artifactId>MavenDemo4</artifactId>
        <version>1.0-SNAPSHOT</version>
        <relativePath>../MavenDemo4/pom.xml</relativePath>
    </parent>
```