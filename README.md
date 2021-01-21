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
6.pom文件的聚合

>定义pom项目

```
 <packaging>pom</packaging>
```

>定义字模块，可以多个

```
<modules>
        <module>ChildPro1</module>
        <module>ChildPro2</module>
</modules>
```

7.maven中setting.xml的配置

>jdk版本的配置:maven全局的配置，以后在创建新的maven项目用的都是jdk1.8的版本配置


```
	<profile>
                <!-- settings.xml中的id不能随便起的 -->
                <!-- 告诉maven我们用jdk1.8 -->
                <id>jdk-1.8</id>
                <!-- 开启JDK的使用 -->
                <activation>
                                <activeByDefault>true</activeByDefault>
                                <jdk>1.8</jdk>
                </activation>
                <properties>
                        <!-- 配置编译器信息 -->
                        <maven.compiler.source>1.8</maven.compiler.source>
                        <maven.compiler.target>1.8</maven.compiler.target>
                        <maven.compiler.compilerVersion>1.8</maven.compiler.compilerVersion>
                </properties>
    </profile>
```

8.maven插件的使用

>在maven项目中更改jdk版本的插件

>#注意：在pom项目时，子模块也是可以单独定义build的，只不过很少有项目会用不同的jdk版本

```
    <!--配置maven的编译器插件-->
    <build>
        <plugins>
            <!--JDK编译插件-->
            <plugin>
                <!--插件坐标-->
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <configuration>
                    <!--源代码使用JDK版本-->
                    <source>8</source>
                    <!--源代码编译为class文件的版本，要保持跟上面版本一致-->
                    <target>8</target>
                    <encoding>UTF-8</encoding>
                </configuration>
            </plugin>
        </plugins>
    </build>
```

9.资源拷贝插件

>配置文件一般都放在：src/main/resource下，打包的时候会打包到target,不放在resource下的，是不会打包进去

>如果把非resource下的文件打包进去的话，需要配置插件

```
<build>
        <resources>
                        <resource>
                                <directory>src/main/java</directory>
                                <includes>
                                        <include>**/*.xml</include>
                                </includes>
                        </resource>
                        <resource>
                                <directory>src/main/resources</directory>
                                <includes>
                                        <include>**/*.xml</include>
                                        <include>**/*.properties</include>
                                </includes>
                        </resource>
                </resources>
</build>

```

10.tomcat插件运行mavenweb项目

>新建maven web项目的时候一定要注意，两个webapp  选择下面的那个别选择coco的那个

>build下可以有两个plugins的，一个是使用的plugins一个是pluginManagement，要注意，使用的plugin要建在plgginmagement外面

```
  <build>
    <plugins>
      <!-- 配置Tomcat插件 -->
      <plugin>
        <groupId>org.apache.tomcat.maven</groupId>
        <artifactId>tomcat7-maven-plugin</artifactId>
        <version>2.2</version>
        <configuration>
          <!-- 配置Tomcat监听端口 -->
          <port>8080</port>
          <!-- 配置项目的访问路径(Application Context) -->
          <path>/</path>
        </configuration>
      </plugin>
    </plugins>
   </bulid>
```

>运行的话，使用maven-》项目-》Plugins->tomcat7:run

11.cmd查看maven版本  

>报错：JAVA_HOME配置的是jre的路径的话，是系统变量配置错误.

>另外，系统变量与用户变量的java环境变量也要与系统的保持一致

12.maven常见的几个命令

>clean:清理打的包；从target目录删除

>install:编译打包部署到本地仓库
```
执行三个操作
-javac
-jar
把jar包放到本地仓库
```

>package:编译打包不部署

>compile:只编译，javac

------到此为止，maven大概重温了一遍，还是学到不少东西，熟悉的感觉又回来了11111111111111111

