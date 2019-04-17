---
layout: post
title: "SpringBoot入门"
date: 2019-04-10
categories: Java SpringBoot
tags: Java SpringBoot Maven Tomcat Idea
---

* content 
{:toc}
# 一、Spring Boot 入门

## 1、Spring Boot 简介

> 简化Spring应用开发的一个框架；
>
> 整个Spring技术栈的一个大整合；
>
> J2EE开发的一站式解决方案；




## 2、微服务

2014，martin fowler

微服务：架构风格（服务微化）

一个应用应该是一组小型服务；可以通过HTTP的方式进行互通；

单体应用：ALL IN ONE

微服务：每一个功能元素最终都是一个可独立替换和独立升级的软件单元；

[详细参照微服务文档](https://martinfowler.com/articles/microservices.html#MicroservicesAndSoa)

## 3、环境准备

<http://www.gulixueyuan.com/> 谷粒学院

环境约束

- jdk1.8：Spring Boot 推荐jdk1.7及以上；java version "1.8.0_112"
- maven3.x：maven 3.3以上版本；Apache Maven 3.3.9
- IntelliJIDEA2017：IntelliJ IDEA 2017.2.2 x64、STS
- SpringBoot 1.5.9.RELEASE：1.5.9；

统一环境；

### 1、MAVEN设置；

给maven 的settings.xml配置文件的profiles标签添加

```xml
<profile>
  <id>jdk-1.8</id>
  <activation>
    <activeByDefault>true</activeByDefault>
    <jdk>1.8</jdk>
  </activation>
  <properties>
    <maven.compiler.source>1.8</maven.compiler.source>
    <maven.compiler.target>1.8</maven.compiler.target>
    <maven.compiler.compilerVersion>1.8</maven.compiler.compilerVersion>
  </properties>
</profile>
```

### 2、IDEA设置

整合maven进来；

## 4、Spring Boot HelloWorld

一个功能：

浏览器发送hello请求，服务器接受请求并处理，响应Hello World字符串；

### 1、创建一个maven工程；（jar）

### 2、导入spring boot相关的依赖

```xml
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>1.5.9.RELEASE</version>
    </parent>
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
    </dependencies>
```

### 3、编写一个主程序：启动Spring Boot应用

```java
@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        
        // Spring应用启动起来
        SpringApplication.run(Application.class, args);
    }
}
```

### 4、编写相关的Controller、Service

```java
@Controller
public class HelloController {

    @ResponseBody
    @RequestMapping("/hello")
    public String hello(){
        return "Hello World!";
    }
}
```

### 5、运行主程序测试

直接右键run`Application`

### 6、简化部署

![SpringBoot-maven-package](https://raw.githubusercontent.com/329213964/329213964.github.io/master/_posts/images/SpringBoot/SpringBoot-maven-package.png)

在pom/xml文件引用插件

```xml
 <!-- 这个插件，可以将应用打包成一个可执行的jar包；-->
    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>
```

导入这个maven插件，利用idea打包，生成的jar包，可以使用`java -jar xxx.jar`启动

Spring Boot 使用嵌入式的Tomcat无需再配置Tomcat

## 5、Hello World探究

### 1、POM文件

#### 1、父项目

```xml
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>1.5.9.RELEASE</version>
</parent>
```

他的父项目是：

```xml
<parent>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-dependencies</artifactId>
  <version>1.5.9.RELEASE</version>
  <relativePath>../../spring-boot-dependencies</relativePath>
</parent>
```

这是真正管理Spring Boot应用里面所依赖的版本

Spring Boot的版本仲裁中心；

以后我们导入依赖默认是不需要写版本；（没有在dependencies里面管理的依赖自然需要声明版本号）

#### 2、启动器

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

**spring-boot-starter-web**：

spring-boot-starter：spring-boot场景启动器，帮我们导入了web模块正常运行所依赖的组件；

点击进去可以看到帮我们引入很多web相关的依赖

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starters</artifactId>
		<version>1.5.4.RELEASE</version>
	</parent>
	<artifactId>spring-boot-starter-web</artifactId>
	<name>Spring Boot Web Starter</name>
	<description>Starter for building web, including RESTful, applications using Spring
		MVC. Uses Tomcat as the default embedded container</description>
	<url>http://projects.spring.io/spring-boot/</url>
	<organization>
		<name>Pivotal Software, Inc.</name>
		<url>http://www.spring.io</url>
	</organization>
	<properties>
		<main.basedir>${basedir}/../..</main.basedir>
	</properties>
	<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-tomcat</artifactId>
		</dependency>
		<dependency>
			<groupId>org.hibernate</groupId>
			<artifactId>hibernate-validator</artifactId>
		</dependency>
		<dependency>
			<groupId>com.fasterxml.jackson.core</groupId>
			<artifactId>jackson-databind</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework</groupId>
			<artifactId>spring-web</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework</groupId>
			<artifactId>spring-webmvc</artifactId>
		</dependency>
	</dependencies>
</project>
```

Spring Boot将所有的功能场景都抽取出来，做成一个个的starters（启动器），只需要在项目里面引入这些starter相关场景的所有依赖都会导入进来，要用什么功能就导入什么场景的启动器

### 2、主程序类，主入口类

```java
package com.atguigu.springboot;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class SpringBoot01HelloworldQuickApplication {

   public static void main(String[] args) {
      SpringApplication.run(SpringBoot01HelloworldQuickApplication.class, args);
   }

}
```

@**SpringBootApplication**:  Spring Boot应用标注在某个类上说明这个类是SpringBoot的主配置类，SpringBoot就改运行这个类的main方法来启用SpringBoot应用；

```java
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Inherited
@SpringBootConfiguration
@EnableAutoConfiguration
@ComponentScan(excludeFilters = {
      @Filter(type = FilterType.CUSTOM, classes = TypeExcludeFilter.class),
      @Filter(type = FilterType.CUSTOM, classes = AutoConfigurationExcludeFilter.class) })
public @interface SpringBootApplication {
```

@**SpringBootConfiguration**:Spring Boot的配置类；

​		标注在某个类上，表示Spring Boot的配置类;

​		@**Configuration**:配置类上标注这个注解；

​			配置类—————配置文件；配置类同样是容器中的一个组件;

@**EnableAutoConfiguration**:开启自动配置；

​		以前需要手动配置的内容，Spring Boot自动配置；

```java
@AutoConfigurationPackage
@Import(AutoConfigurationImportSelector.class)
public @interface EnableAutoConfiguration {
```

@**AutoConfigurationPackage**:自动配置包；

​		@**Import**(AutoConfigurationPackages.Registrar.class)；

​		Spring 底层注解@import,给容器导入一个组件；导入组件由AutoConfigurationPackages.Registrar.class

==将主配置类(@SpringBootApplication标注的类)所在包底下所有子包内的组件扫描到Spring容器中；==

​		@Import(AutoConfigurationImportSelector.class);

​			给容器中导入组件？

​			AutoConfigurationImportSelector：导入组件的选择器；

​			将所有需要导入的组件以全类名的方式返回，这些组件就会被添加到容器中；

​			给容器导入许多的自动配置类(xxxAutoConfiguration)；就是给容器导入这个场景需要的所有组件，并配置好这些组件；

​		![AutoConfigurationImportSelector-debug](https://raw.githubusercontent.com/329213964/329213964.github.io/master/_posts/images/SpringBoot/SpringBoot-AutoConfigurationImportSelector-debug.png)

有了自动配置类，免去了我们手动配置填写注入功能组件等工作；

​		SpringFactoriesLoader.loadFactoryNames(EnableAutoConfiguration.class,classLoader);

==Spring Boot在启动时从类路径下的META-INF/spring.factories中获取EnableAutoConfiguration指定的值;将这些值作为自动配置类导入到容器中，自动配置类生效，帮我们进行自动配置工作;==以前需要自己配置的内容，Spring Boot帮我们做了；

## 6、使用Spring Initializer快速创建Spring Boot项目

IDEA都支持Spring的项目创建向导快速创建一个Spring Boot项目：

![Spring Initializer1](https://raw.githubusercontent.com/329213964/329213964.github.io/master/_posts/images/SpringBoot/SpringBoot-Spring Initializer1.png)

![](https://raw.githubusercontent.com/329213964/329213964.github.io/master/_posts/images/SpringBoot/SpringBoot-Spring Initializer2.png)

![](https://raw.githubusercontent.com/329213964/329213964.github.io/master/_posts/images/SpringBoot/SpringBoot-Spring Initializer3.png)

选择所需的模块创建即可；向导联网创建出Spring Boot项目；

默认生成的Spring Boot项目；

* 主程序已生成，只需逻辑
* resourcers文件夹中目录结构
  * static：保存所有的静态资源;js css images;
  * templates:保存所有的模板页面;（Spring Boot默认jar包使用嵌入式的Tomcat，默认不支持JSP页面）；可以使用模板引擎（freemarker、thymeleaf）;
  * application.properties:Spring Boot配置文件；可以修改一些默认的配置；

# 二、配置文件

## 1、配置文件

SpringBoot使用一个全局的配置文件,配置文件名固定

* application.properties
* application.yml



配置文件作用：修改SpringBoot自动配置的默认值；

YAML（YAML Ain't Markup Language）

​	YAML A Markup Language：是一个标记语言

​	YAML isn't Markup Language：不是一个标记语言

标记语言：

​	以前的配置文件：xxxx.xml;

​	YAML：以数据为中心，比json、xml更适合作为配置文件\

​	YAML：配置例子

```yaml
server:
  port: 80
```

​	XML:

```xml
<server>
	<port>80</port>
</server>
```

## 2、YAML语法：

### 1、基本语法

key:[空格]value: 表示一对键值对（空格必须有）;

以空格的缩进来控制层级关系；只要是左对齐的一列数据，都是同一个层级的

```yaml
server:
	port: 80
	path: /hello
```

属性和值大小写敏感;(属性和值之间也有空格)

### 2、值的写法

**字面量；普通的值（数字，字符串，布尔）**

​	k: v: 字面直接来写；

​		字符串默认不同加上单引号或者双引号；

​		“”：双引号：不会转义特殊字符串里的特殊字符；字符串会作为本身想表示的意思；

​			name:“zhangsan \n list”：输出：zhangsan 换行 list

​		''：单引号：转义特殊字符，特殊字符最终以字符串输出

​			name:“zhangsan \n list”：输出：zhangsan \n list

**对象（属性和值）（键值对）：**

​	k: v:在下一行写对象的属性和值的关系；注意缩进

​		对象还是k: v:的方式

```yaml
friends:
	lastname: zhangsan
	age: 20
```

行内写法：

```yaml
friends: {lastname: zhangsan,age: 18}
```



**数组（List、Set）:**

用-值表示数组中的一个元素

```yaml
pets:
 - cat
 - dog
 - pig
```

行内写法：

```yaml
pets: [cat,dog,pig]
```

##3、配置文件值注入

配置文件

```yaml
person:
  lastName: zhangsan
  age: 18
  boss: false
  birth: 2012/12/12
  maps: {k1: v1,k2: 12}
  lists:
    - lisi
    - zhaoliu
  dog:
    name: fox
    age: 2
```

javaBean:

```java
/**
 * 将配置文件中的配置的每一个属性的值，映射到这个组件中
 * @ConfigurationProperties：告诉SpringBoot将本类中的所有属性和配置文件中的相关配置进行绑定；
 *      prefix = "person"：配置文件中那个下面的所有属性进行一一映射
 *
 * 只有这个组件是容器中的组件，才能使用容器提供的@ConfigurationProperties功能;
 *
 */
@Component
@ConfigurationProperties(prefix = "person")
public class Person {
    private String lastName;
    private Integer age;
    private Boolean boss;
    private Date birth;

    private Map<String,Object> maps;
    private List<Object> lists;
    private Dog dog;
```



可以导入配置文件处理器，编写配置将有提示

```xml
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-configuration-processor</artifactId>
			<optional>true</optional>
		</dependency>
```

###1、properties配置文件在idea中可能乱码

###2、@value获取值和@ConfigurationProperties获取值比较

|                      | @ConfigurationProperties | @Value     |
| -------------------- | ------------------------ | ---------- |
| 功能                 | 批量注入配置文件中的属性 | 一个个指定 |
| 松散绑定（松散语法） | 支持                     | 不支持     |
| SpEL                 | 不支持                   | 支持       |
| JSR303数据校验       | 支持                     | 不支持     |
| 复杂类型封装         | 支持                     | 不支持     |

配置文件yml还是properties他们都能获取到值；

如果，只是在某个业务逻辑中需要获取配置文件中的某项值，使用@Value

如果，专门编写了一个javaBean来和配置文件进行映射，我们就直接使用@ConfigurationProperties；

###3、配置文件注入值数据校验

```java
@Component
@ConfigurationProperties(prefix = "person")
@Validated
public class Person {
    @Email
    private String lastName;
    private Integer age;
    private Boolean boss;
    private Date birth;

    private Map<String,Object> maps;
    private List<Object> lists;
    private Dog dog;
```



###4、@PropertySource&@ImportResource

@**PropertySource**：加载指定配置文件；

```java
@PropertySource(value = {"classpath:person.properties"})
@Component
@ConfigurationProperties(prefix = "person")
//@Validated
public class Person {
//    @Email
    private String lastName;
    private Integer age;
    private Boolean boss;
    private Date birth;

    private Map<String,Object> maps;
    private List<Object> lists;
    private Dog dog;

```

@**ImportResource**：导入Spring的配置文件，让配置文件里面的内容生效；

Spring Boot里面没有Spring的配置文件，我们自己编写的配置文件，也不能自动识别；

想让Spring配置文件生效，加载其；@**ImportResource**标注在一个配置类上；

```java
@ImportReSource(locations = {"classpath:beans.xml"})
导入Spring配置文件让其生效
```



不来编写Spring的配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="helloService" class="com.atguigu.springboot.service.HelloService"></bean>


</beans>
```

SpringBoot推荐给容器中添加组件的方式；推荐使用全注解的方式；

1、配置类====Spring配置文件

2、使用@Bean给容器中添加组件

```java
@Configuration
public class myAppConfig {

    @Bean
    public HelloService helloService(){
        System.out.println("配置类@Bean给容器中添加组件");
        return new HelloService();
    }
}
```



##4、配置文件占位符

###1、随机数

```java
random.value、{random.int}、$(random.long)
random.int(10)、{random.int[1024,65536]}

```

###2、占位符获取之前配置的值，如果没有可以使用：指定默认值

```properties
person.last-name=宗三${random.uuid}
person.age=${random.int}
person.birth=2012/12/12
person.boss=false
person.maps.k1=v1
person.maps.k2=14
person.lists=a,b,c
person.dog.name=${person.hello:hello}_dog
person.dog.age=15
```

##5、Profile

###1、多Profile文件

在主配置文件编写时，文件名可以是application-{profile}.properties/yml

默认使用application.properties的配置



###2、yml支持多文档块方式

```yaml
server:
  port: 80
spring:
  profiles:
    active: prod
---
server:
  port: 8083
spring:
  profiles: dev

---
server:
  port: 8084
spring:
  profiles: prod #指定属于哪个文档块
```



###3、激活指定profile

​	1、在配置文件中指定 spring.profiles.active-dev

​	2、命令行：

​		java -jar spring-boot-02-config-0.0.1-SNAPSHOT.jar --spring.profiles.active=dev;

​		可以直接在测试时，配置传入命令行参数

​	3、虚拟的参数：

​		-Dspring.profiles.active=dev



##6、配置文件加载位置

springboot启动会扫描以下位置的application.properties或者application.yml作为Spring boot的默认配置文件

-file:./config

-file:./

-classpath:/config/

-classpath:/

优先级由高到低，高优先级的配置覆盖低优先级的配置；

SpringBoot会从这四个位置全部加载主配置文件；形成**互补配置**;



==我们可以通过spring.config.location来改变默认的文件配置==

**项目打包好以后，我们可以使用命令行参数的形式，启动项目的时候来指定配置文件的新位置；指定配置文件和默认加载的这些配置文件共同起作用形成互补配置；**



##7、外部配置加载顺序

**SpringBoot也可以从以下位置加载配置；优先级从高到低；高优先级的配置覆盖低优先级的配置，所有的配置会形成互补配置**

1、命令行参数

java -jar spring-boot-02-config-02-0.0.1-SNAPSHOT.jar --server.port=8087

多个配置用空格分开；--配置项=值



2、来自java:comp/env的NDI属性

3、Java系统属性（System.getProperties()）

4、操作系统环境变量

5、RandomValuePropertySource配置的random.*属性值



==**由jar包外向jar包内进行寻找；**==

==**优先加载带profile**==

**6、jar包外部的application-{profile}.properties或application.yml(带spring.profile)配置文件**

**7、jar包内部的application-{profile}.properties或application.yml(带spring.profile)配置文件**



==**再来加载不带profile**==

**8、jar包外部的application.properties或application.yml(不带spring.profile)配置文件**

**9、jar包内部的application.properties或application.yml(不带spring.profile)配置文件**

10、@Configuration注解类上的@PropertySource

11、通过SpringApplication.setDefaultProperties指定的默认属性

所有支持的配置加载来源；

[参考官方文档](https://docs.spring.io/spring-boot/docs/2.0.9.BUILD-SNAPSHOT/reference/htmlsingle/#getting-started-first-application-executable-jar )

## ==8、自动配置原理(SpringBoot精华所在)==

配置文件到底能写什么？怎么写？自动配置原理；

[配置文件能配置的属性参照](https://docs.spring.io/spring-boot/docs/2.0.9.BUILD-SNAPSHOT/reference/htmlsingle/#common-application-properties )



### 1、自动配置原理：

1）、SpringBoot启动的时候加载主配置类，开启了自动配置功能==@EnableAutoConfiguration==

2）、@EnableAutoConfiguration 作用：

* 利用AutoConfigurationImportSelector给容器导入组件

* 可以查看selectImports()方法的内容；

* List<String>configurations=getCandidateConfigurations(annotationMetadata,attributes)获取候选的配置

  * ```java
    SpringFactoriesLoader.loadFactoryNames();
    //扫描所有jar包类路径下 META-INF/spring.factories
    //把扫描到的这些文件的内容包装成properties对象
    //从properties中获取到EnableAutoConfiguration.class类（类名）对应的值，把他们添加在容器中
    ```



​	==**将类路径下META-INF/spring.factories里面配置的所有EnableAutoConfiguration的值加入到了容器中**==

```properties
# Auto Configure
org.springframework.boot.autoconfigure.EnableAutoConfiguration=\
org.springframework.boot.autoconfigure.admin.SpringApplicationAdminJmxAutoConfiguration,\
org.springframework.boot.autoconfigure.aop.AopAutoConfiguration,\
org.springframework.boot.autoconfigure.amqp.RabbitAutoConfiguration,\
org.springframework.boot.autoconfigure.batch.BatchAutoConfiguration,\
org.springframework.boot.autoconfigure.cache.CacheAutoConfiguration,\
org.springframework.boot.autoconfigure.cassandra.CassandraAutoConfiguration,\
org.springframework.boot.autoconfigure.cloud.CloudServiceConnectorsAutoConfiguration,\
org.springframework.boot.autoconfigure.context.ConfigurationPropertiesAutoConfiguration,\
org.springframework.boot.autoconfigure.context.MessageSourceAutoConfiguration,\
org.springframework.boot.autoconfigure.context.PropertyPlaceholderAutoConfiguration,\
org.springframework.boot.autoconfigure.couchbase.CouchbaseAutoConfiguration,\
org.springframework.boot.autoconfigure.dao.PersistenceExceptionTranslationAutoConfiguration,\
org.springframework.boot.autoconfigure.data.cassandra.CassandraDataAutoConfiguration,\
org.springframework.boot.autoconfigure.data.cassandra.CassandraReactiveDataAutoConfiguration,\
org.springframework.boot.autoconfigure.data.cassandra.CassandraReactiveRepositoriesAutoConfiguration,\
org.springframework.boot.autoconfigure.data.cassandra.CassandraRepositoriesAutoConfiguration,\
org.springframework.boot.autoconfigure.data.couchbase.CouchbaseDataAutoConfiguration,\
org.springframework.boot.autoconfigure.data.couchbase.CouchbaseReactiveDataAutoConfiguration,\
org.springframework.boot.autoconfigure.data.couchbase.CouchbaseReactiveRepositoriesAutoConfiguration,\
org.springframework.boot.autoconfigure.data.couchbase.CouchbaseRepositoriesAutoConfiguration,\
org.springframework.boot.autoconfigure.data.elasticsearch.ElasticsearchAutoConfiguration,\
org.springframework.boot.autoconfigure.data.elasticsearch.ElasticsearchDataAutoConfiguration,\
org.springframework.boot.autoconfigure.data.elasticsearch.ElasticsearchRepositoriesAutoConfiguration,\
org.springframework.boot.autoconfigure.data.jdbc.JdbcRepositoriesAutoConfiguration,\
org.springframework.boot.autoconfigure.data.jpa.JpaRepositoriesAutoConfiguration,\
org.springframework.boot.autoconfigure.data.ldap.LdapRepositoriesAutoConfiguration,\
org.springframework.boot.autoconfigure.data.mongo.MongoDataAutoConfiguration,\
org.springframework.boot.autoconfigure.data.mongo.MongoReactiveDataAutoConfiguration,\
org.springframework.boot.autoconfigure.data.mongo.MongoReactiveRepositoriesAutoConfiguration,\
org.springframework.boot.autoconfigure.data.mongo.MongoRepositoriesAutoConfiguration,\
org.springframework.boot.autoconfigure.data.neo4j.Neo4jDataAutoConfiguration,\
org.springframework.boot.autoconfigure.data.neo4j.Neo4jRepositoriesAutoConfiguration,\
org.springframework.boot.autoconfigure.data.solr.SolrRepositoriesAutoConfiguration,\
org.springframework.boot.autoconfigure.data.redis.RedisAutoConfiguration,\
org.springframework.boot.autoconfigure.data.redis.RedisReactiveAutoConfiguration,\
org.springframework.boot.autoconfigure.data.redis.RedisRepositoriesAutoConfiguration,\
org.springframework.boot.autoconfigure.data.rest.RepositoryRestMvcAutoConfiguration,\
org.springframework.boot.autoconfigure.data.web.SpringDataWebAutoConfiguration,\
org.springframework.boot.autoconfigure.elasticsearch.jest.JestAutoConfiguration,\
org.springframework.boot.autoconfigure.elasticsearch.rest.RestClientAutoConfiguration,\
org.springframework.boot.autoconfigure.flyway.FlywayAutoConfiguration,\
org.springframework.boot.autoconfigure.freemarker.FreeMarkerAutoConfiguration,\
org.springframework.boot.autoconfigure.gson.GsonAutoConfiguration,\
org.springframework.boot.autoconfigure.h2.H2ConsoleAutoConfiguration,\
org.springframework.boot.autoconfigure.hateoas.HypermediaAutoConfiguration,\
org.springframework.boot.autoconfigure.hazelcast.HazelcastAutoConfiguration,\
org.springframework.boot.autoconfigure.hazelcast.HazelcastJpaDependencyAutoConfiguration,\
org.springframework.boot.autoconfigure.http.HttpMessageConvertersAutoConfiguration,\
org.springframework.boot.autoconfigure.http.codec.CodecsAutoConfiguration,\
org.springframework.boot.autoconfigure.influx.InfluxDbAutoConfiguration,\
org.springframework.boot.autoconfigure.info.ProjectInfoAutoConfiguration,\
org.springframework.boot.autoconfigure.integration.IntegrationAutoConfiguration,\
org.springframework.boot.autoconfigure.jackson.JacksonAutoConfiguration,\
org.springframework.boot.autoconfigure.jdbc.DataSourceAutoConfiguration,\
org.springframework.boot.autoconfigure.jdbc.JdbcTemplateAutoConfiguration,\
org.springframework.boot.autoconfigure.jdbc.JndiDataSourceAutoConfiguration,\
org.springframework.boot.autoconfigure.jdbc.XADataSourceAutoConfiguration,\
org.springframework.boot.autoconfigure.jdbc.DataSourceTransactionManagerAutoConfiguration,\
org.springframework.boot.autoconfigure.jms.JmsAutoConfiguration,\
org.springframework.boot.autoconfigure.jmx.JmxAutoConfiguration,\
org.springframework.boot.autoconfigure.jms.JndiConnectionFactoryAutoConfiguration,\
org.springframework.boot.autoconfigure.jms.activemq.ActiveMQAutoConfiguration,\
org.springframework.boot.autoconfigure.jms.artemis.ArtemisAutoConfiguration,\
org.springframework.boot.autoconfigure.groovy.template.GroovyTemplateAutoConfiguration,\
org.springframework.boot.autoconfigure.jersey.JerseyAutoConfiguration,\
org.springframework.boot.autoconfigure.jooq.JooqAutoConfiguration,\
org.springframework.boot.autoconfigure.jsonb.JsonbAutoConfiguration,\
org.springframework.boot.autoconfigure.kafka.KafkaAutoConfiguration,\
org.springframework.boot.autoconfigure.ldap.embedded.EmbeddedLdapAutoConfiguration,\
org.springframework.boot.autoconfigure.ldap.LdapAutoConfiguration,\
org.springframework.boot.autoconfigure.liquibase.LiquibaseAutoConfiguration,\
org.springframework.boot.autoconfigure.mail.MailSenderAutoConfiguration,\
org.springframework.boot.autoconfigure.mail.MailSenderValidatorAutoConfiguration,\
org.springframework.boot.autoconfigure.mongo.embedded.EmbeddedMongoAutoConfiguration,\
org.springframework.boot.autoconfigure.mongo.MongoAutoConfiguration,\
org.springframework.boot.autoconfigure.mongo.MongoReactiveAutoConfiguration,\
org.springframework.boot.autoconfigure.mustache.MustacheAutoConfiguration,\
org.springframework.boot.autoconfigure.orm.jpa.HibernateJpaAutoConfiguration,\
org.springframework.boot.autoconfigure.quartz.QuartzAutoConfiguration,\
org.springframework.boot.autoconfigure.reactor.core.ReactorCoreAutoConfiguration,\
org.springframework.boot.autoconfigure.security.servlet.SecurityAutoConfiguration,\
org.springframework.boot.autoconfigure.security.servlet.SecurityRequestMatcherProviderAutoConfiguration,\
org.springframework.boot.autoconfigure.security.servlet.UserDetailsServiceAutoConfiguration,\
org.springframework.boot.autoconfigure.security.servlet.SecurityFilterAutoConfiguration,\
org.springframework.boot.autoconfigure.security.reactive.ReactiveSecurityAutoConfiguration,\
org.springframework.boot.autoconfigure.security.reactive.ReactiveUserDetailsServiceAutoConfiguration,\
org.springframework.boot.autoconfigure.sendgrid.SendGridAutoConfiguration,\
org.springframework.boot.autoconfigure.session.SessionAutoConfiguration,\
org.springframework.boot.autoconfigure.security.oauth2.client.servlet.OAuth2ClientAutoConfiguration,\
org.springframework.boot.autoconfigure.security.oauth2.client.reactive.ReactiveOAuth2ClientAutoConfiguration,\
org.springframework.boot.autoconfigure.security.oauth2.resource.servlet.OAuth2ResourceServerAutoConfiguration,\
org.springframework.boot.autoconfigure.security.oauth2.resource.reactive.ReactiveOAuth2ResourceServerAutoConfiguration,\
org.springframework.boot.autoconfigure.solr.SolrAutoConfiguration,\
org.springframework.boot.autoconfigure.task.TaskExecutionAutoConfiguration,\
org.springframework.boot.autoconfigure.task.TaskSchedulingAutoConfiguration,\
org.springframework.boot.autoconfigure.thymeleaf.ThymeleafAutoConfiguration,\
org.springframework.boot.autoconfigure.transaction.TransactionAutoConfiguration,\
org.springframework.boot.autoconfigure.transaction.jta.JtaAutoConfiguration,\
org.springframework.boot.autoconfigure.validation.ValidationAutoConfiguration,\
org.springframework.boot.autoconfigure.web.client.RestTemplateAutoConfiguration,\
org.springframework.boot.autoconfigure.web.embedded.EmbeddedWebServerFactoryCustomizerAutoConfiguration,\
org.springframework.boot.autoconfigure.web.reactive.HttpHandlerAutoConfiguration,\
org.springframework.boot.autoconfigure.web.reactive.ReactiveWebServerFactoryAutoConfiguration,\
org.springframework.boot.autoconfigure.web.reactive.WebFluxAutoConfiguration,\
org.springframework.boot.autoconfigure.web.reactive.error.ErrorWebFluxAutoConfiguration,\
org.springframework.boot.autoconfigure.web.reactive.function.client.ClientHttpConnectorAutoConfiguration,\
org.springframework.boot.autoconfigure.web.reactive.function.client.WebClientAutoConfiguration,\
org.springframework.boot.autoconfigure.web.servlet.DispatcherServletAutoConfiguration,\
org.springframework.boot.autoconfigure.web.servlet.ServletWebServerFactoryAutoConfiguration,\
org.springframework.boot.autoconfigure.web.servlet.error.ErrorMvcAutoConfiguration,\
org.springframework.boot.autoconfigure.web.servlet.HttpEncodingAutoConfiguration,\
org.springframework.boot.autoconfigure.web.servlet.MultipartAutoConfiguration,\
org.springframework.boot.autoconfigure.web.servlet.WebMvcAutoConfiguration,\
org.springframework.boot.autoconfigure.websocket.reactive.WebSocketReactiveAutoConfiguration,\
org.springframework.boot.autoconfigure.websocket.servlet.WebSocketServletAutoConfiguration,\
org.springframework.boot.autoconfigure.websocket.servlet.WebSocketMessagingAutoConfiguration,\
org.springframework.boot.autoconfigure.webservices.WebServicesAutoConfiguration,\
org.springframework.boot.autoconfigure.webservices.client.WebServiceTemplateAutoConfiguration
```

每一个这样的xxxAutoConfiguration类都是容器中的一个组件，都加入到容器中；用他们来做自动配置；

3）、每个自动配置类进行自动配置功能

4）、以**HttpEncodingAutoConfiguration（Http编码自动配置）**为例解释自动配置原理；

```java
@Configuration //表示这是一个配置类，类似于以前编写的配置文件，也可以给容器中添加组件
@EnableConfigurationProperties(HttpProperties.class)//启用指定类的configurationProperties功能；将配置文件中对应的值和HttpProperties绑定起来；并把HttpProperties加入到ioc容器中；

@ConditionalOnWebApplication(type = ConditionalOnWebApplication.Type.SERVLET)//Spring底层@Conditional注解，根据不同的条件，如果满足指定的条件，整个配置类里面的配置就会生效； 判断当前应用是否是web应用，如果是，当前配置类生效

@ConditionalOnClass(CharacterEncodingFilter.class)//判断当前项目有没有这个类 CharacterEncodingFilter；SpringMVC中进行乱码解决的过滤器；
@ConditionalOnProperty(prefix = "spring.http.encoding", value = "enabled",
		matchIfMissing = true)//配置文件中是否存在某个配置spring.http.encoding.enabled；如果不存在判断也是成立的
//即使我们配置文件中不配置spring.http.encoding.enabled,也是默认生效的;
public class HttpEncodingAutoConfiguration {
    
    //已经和SpringBoot的配置文件映射了
    private final HttpProperties.Encoding properties;
    
    //只有一个有参构造器的情况下，参数的值就会从容器中拿
    public HttpEncodingAutoConfiguration(HttpProperties properties) {
		this.properties = properties.getEncoding();
	}

    
    @Bean  //给容器中添加一个组件，这个组件某些值需要从properties中获取；
	@ConditionalOnMissingBean
	public CharacterEncodingFilter characterEncodingFilter() {
		CharacterEncodingFilter filter = new OrderedCharacterEncodingFilter();
		filter.setEncoding(this.properties.getCharset().name());
		filter.setForceRequestEncoding(this.properties.shouldForce(Type.REQUEST));
		filter.setForceResponseEncoding(this.properties.shouldForce(Type.RESPONSE));
		return filter;
	}
```

根据当前不同的条件判断，决定这个配置类是否生效；

一旦这个配置类生效；这个配置类就会给容器中添加各种组件；这些组件的属性是从对应的properties类中获取的，这些类里面的每一个属性又是和配置文件绑定的；

5）、所有在配置文件中能配置的属性都是在xxxProperties类中封装着；配置文件能配置什么就可以参照某个功能对应的这个属性类

```java
@ConfigurationProperties(prefix = "spring.http")  //从配置文件中获取指定的值和bean的属性进行绑定
public class HttpProperties {
```



**精髓：**

​	**1）、SpringBoot启动会加载大量的自动配置类**

​	**2）、我们看我们需要的功能有没有SpringBoot默认写好的自动配置类；**

​	**3）、再来看这个自动配置类中到底配置了哪些组件（只要我们要用的组件有，我们就不需要再来配置了）**

​	**4）给容器中自动配置类中添加组件时，会从properties类中获取某些属性，我们可以在配置文件中指定这些属性的值；**



xxxAutoConfiguration:自动配置类；

给容器中添加组件；

xxxProperties：封装配置文件中的相关属性；



### 2、细节

#### 1、@Conditional派生注解（Spring注解版原生的@Conditional作用）

作用：必须是@Conditional指定的条件成立，才给容器中添加组件，配置配的所有内容才会生效；

| @Conditional派生注解            | 作用（判断是否满足当前指定条件）                |
| ------------------------------- | ----------------------------------------------- |
| @ConditionalOnJava              | 系统的java版本是否符合要求                      |
| @ConditionalOnBean              | 容器中存在指定Bean                              |
| @ConditionalOnMissBean          | 容器中不存在指定Bean                            |
| @ConditionalOnExpression        | 满足spEL表达式                                  |
| @ConditionalOnClass             | 系统中有指定的类                                |
| @ConditionalOnMissClass         | 系统中没有指定的类                              |
| @ConditionalOnSingleCandidate   | 容器中只有一个指定的Bean,或者这个Bean是首选Bean |
| @ConditionalOnProperty          | 系统中指定的属性是否有指定的值                  |
| @ConditionalOnResource          | 类路径下是否存在指定的资源文件                  |
| @ConditionalOnWebApplication    | 当前是web环境                                   |
| @ConditionalOnNotWebApplication | 当前不是web环境                                 |
| @ConditionalOnJndi              | JNDI存在指定项                                  |

**自动配置类必须在一定的条件下才能生效；**

如何知道哪些自动配置类生效了？

我们可以通过启用debug=true属性；来让控制台打印自动配置报告，这样我们就可以很方便的自动哪些自动配置类生效；

```java
============================

CONDITIONS EVALUATION REPORT
============================


Positive matches:（启动的，匹配成功的）
-----------------

   CodecsAutoConfiguration matched:
      - @ConditionalOnClass found required class 'org.springframework.http.codec.CodecConfigurer'; @ConditionalOnMissingClass did not find unwanted class (OnClassCondition)
        ......
        
 Negative matches:（没有启动的，没有匹配成功的）
-----------------

   ActiveMQAutoConfiguration:
      Did not match:
         - @ConditionalOnClass did not find required classes 'javax.jms.ConnectionFactory', 'org.apache.activemq.ActiveMQConnectionFactory' (OnClassCondition)
.....
```





# 三、日志

## 1、日志框架

小张；开发一个大型系统；

​	1、System.out.println("")；将关键数据打印在控制台；去掉？写在一个文件？

​	2、框架来记录系统的一些运行是信息；日志框架；zhanglogging.jar;

​	3、高大上的几个功能？异步模式？自动归档？xxxx？zhanglogging-goog.jar?

​	4、将以前的框架卸下来？换上新的框架，重新修改之前相关的API；zhanglogging-perfect.jar;

​	5、JDBC---数据库驱动；

​		写了一个统一个接口层；日志门面（日志的一个抽象层）；logging-abstract.jar；

​		给项目中导入具体的日志实现就行了；我们之前的日志框架都是实现的抽象层；

市面上的日志框架；

JUL、JCL、Jboss-logging、logback、log4j、log4j2、slf4j.....

| 日志抽象层                                                   | 日志实现                                        |
| ------------------------------------------------------------ | ----------------------------------------------- |
| ~~JCL(Jakarta Commons Logging)~~ SLF4j(Simple Logging Facade for Java) ~~jboss-logging~~ | Log4j ~~JUL(java.util.logging)~~ Log4j2 Logback |

左边选一个门面（抽象层）、右边来选一个实现；

日志门面：SLF4j；

日志实现：Logback；



SpringBoot：底层是Spring框架，Spring框架默认是用JCL；

​	==**SpringBoot选用SLF4j和logback；**==



## 2、SLF4j使用

### 1、如何在系统中使用SLF4j

以后开发的时候，日志记录方法调用，不应该直接调用日志实现类，而是调用日志抽象层里的方法；

给系统导入SLF4j的jar以及logback的实现jar

```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class HelloWorld {
  public static void main(String[] args) {
    Logger logger = LoggerFactory.getLogger(HelloWorld.class);
    logger.info("Hello World");
  }
}
```

图示：

![](https://raw.githubusercontent.com/329213964/329213964.github.io/master/_posts/images/SLF4J/concrete-bindings.png)

每一个日志实现框架都有自己的配置文件，使用SLF4J以后，**配置文件还是做成日志实现框架的配置文件；**



### 2、遗留问题

a:（slf4j+logback）：Spring(commons-logging)、Hibernate（jboss-logging）、MyBatis、xxxx

统一日志记录，即使是别的框架也统一使用slf4j进行输出？

![](https://raw.githubusercontent.com/329213964/329213964.github.io/master/_posts/images/SLF4J/legacy.png)



**如何让系统中所有的日志都统一到slf4j;**

==1、将系统中的其他日志框架先排除出去；==

==2、用中间包来替换原有的日志框架；==

==3、我们导入slf4j其他的实现；==