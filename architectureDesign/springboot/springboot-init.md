# 1、初始化Web工程

![1540450624149](C:\Users\w_fancw\Desktop\springboot\assets\1540450624149.png)

![1540450842937](C:\Users\w_fancw\Desktop\springboot\assets\1540450842937.png)

## 1.1、jar包模式

![1540450985715](C:\Users\w_fancw\Desktop\springboot\assets\1540450985715.png)

![1540451326181](C:\Users\w_fancw\Desktop\springboot\assets\1540451326181.png)



![1540451464759](C:\Users\w_fancw\Desktop\springboot\assets\1540451464759.png)

**注意：SpringBoot的版本改为2.0.4（Mybatis Plus使用2.0.6这个版本的SpringBoot会报错）**



## 1.2、去掉不需要的文件

![1540451538186](C:\Users\w_fancw\Desktop\springboot\assets\1540451538186.png)

删除静态文件目录

![1540451595954](C:\Users\w_fancw\Desktop\springboot\assets\1540451595954.png)

## 1.2、创建Controller

![1540451750331](C:\Users\w_fancw\Desktop\springboot\assets\1540451750331.png)

![1540451797197](C:\Users\w_fancw\Desktop\springboot\assets\1540451797197.png)

![1540451876376](C:\Users\w_fancw\Desktop\springboot\assets\1540451876376.png)

> @RestController：rest风格的请求与响应。
>
> @GetMapping：接受get请求。

## 1.3、测试

![1540452003940](C:\Users\w_fancw\Desktop\springboot\assets\1540452003940.png)

# 2、全局配置

## 2.1、配置文件(开发、生产)

![1540452418969](C:\Users\w_fancw\Desktop\springboot\assets\1540452418969.png)

## 2.2、logback

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!--
scan：当此属性设置为true时，配置文件如果发生改变，将会被重新加载，默认值为true。
scanPeriod：设置监测配置文件是否有修改的时间间隔，如果没有给出时间单位，默认单位是毫秒当scan为true时，此属性生效。默认的时间间隔为1分钟。
debug：当此属性设置为true时，将打印出logback内部日志信息，实时查看logback运行状态。默认值为false。
-->
<configuration scan="true" scanPeriod="60 seconds" debug="false">
    <!-- 定义日志的根目录 -->
    <springProfile name="dev">
        <property name="LOG_HOME" value="D:\logs" />
    </springProfile>
    <springProfile name="!dev">
        <property name="LOG_HOME" value="D:\logs" />
    </springProfile>
    <!-- 定义日志文件名称 -->
    <property name="appName" value="tkbb"></property>
    <!-- ch.qos.logback.core.ConsoleAppender 表示控制台输出 -->
    <appender name="stdout" class="ch.qos.logback.core.ConsoleAppender">
        <!--
        日志输出格式：
			%d表示日期时间，
			%thread表示线程名，
			%-5level：级别从左显示5个字符宽度
			%logger{50} 表示logger名字最长50个字符，否则按照句点分割。 
			%msg：日志消息，
			%n是换行符
        -->
        <layout class="ch.qos.logback.classic.PatternLayout">
            <pattern>%d{yyyy-MM-dd HH:mm:ss.SSS} [ %thread ] - [ %-5level ] [ %logger{50} : %line ] - %msg%n</pattern>
        </layout>
    </appender>

    <!-- 滚动记录文件，先将日志记录到指定文件，当符合某个条件时，将日志记录到其他文件 -->  
    <appender name="appLogAppender" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <!-- 指定日志文件的名称 -->
        <file>${LOG_HOME}/${appName}.log</file>
        <!--
        当发生滚动时，决定 RollingFileAppender 的行为，涉及文件移动和重命名
        TimeBasedRollingPolicy： 最常用的滚动策略，它根据时间来制定滚动策略，既负责滚动也负责出发滚动。
        -->
        <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
            <!--
            滚动时产生的文件的存放位置及文件名称 %d{yyyy-MM-dd}：按天进行日志滚动 
            %i：当文件大小超过maxFileSize时，按照i进行文件滚动
            -->
            <fileNamePattern>${LOG_HOME}/${appName}-%d{yyyy-MM-dd}-%i.log</fileNamePattern>
            <!-- 
            可选节点，控制保留的归档文件的最大数量，超出数量就删除旧文件。假设设置每天滚动，
            且maxHistory是365，则只保存最近365天的文件，删除之前的旧文件。注意，删除旧文件是，
            那些为了归档而创建的目录也会被删除。
            -->
            <MaxHistory>365</MaxHistory>
            <!-- 
            当日志文件超过maxFileSize指定的大小是，根据上面提到的%i进行日志文件滚动 注意此处配置SizeBasedTriggeringPolicy是无法实现按文件大小进行滚动的，必须配置timeBasedFileNamingAndTriggeringPolicy
            -->
            <timeBasedFileNamingAndTriggeringPolicy class="ch.qos.logback.core.rolling.SizeAndTimeBasedFNATP">
                <maxFileSize>100MB</maxFileSize>
            </timeBasedFileNamingAndTriggeringPolicy>
        </rollingPolicy>
        <!-- 日志输出格式： -->     
        <layout class="ch.qos.logback.classic.PatternLayout">
            <pattern>%d{yyyy-MM-dd HH:mm:ss.SSS} [ %thread ] - [ %-5level ] [ %logger{50} : %line ] - %msg%n</pattern>
        </layout>
    </appender>

    <!-- 
		logger主要用于存放日志对象，也可以定义日志类型、级别
		name：表示匹配的logger类型前缀，也就是包的前半部分
		level：要记录的日志级别，包括 TRACE < DEBUG < INFO < WARN < ERROR
		additivity：作用在于children-logger是否使用 rootLogger配置的appender进行输出，
		false：表示只用当前logger的appender-ref，true：
		表示当前logger的appender-ref和rootLogger的appender-ref都有效
    -->
    <!-- hibernate logger -->
    <logger name="cn.com.yusys.tkbb" level="debug" />
    <!-- Spring framework logger -->
    <logger name="org.springframework" level="info" additivity="true"></logger>



    <!-- 
    root与logger是父子关系，没有特别定义则默认为root，任何一个类只会和一个logger对应，
    要么是定义的logger，要么是root，判断的关键在于找到这个logger，然后判断这个logger的appender和level。 
    -->
    <root level="debug">
        <appender-ref ref="stdout" />
        <appender-ref ref="appLogAppender" />
    </root>
</configuration> 
```



![1540452572400](C:\Users\w_fancw\Desktop\springboot\assets\1540452572400.png)

## 2.3、banner

```html
$$$$$$$$\        $$\       $$\   $$\                              
\__$$  __|       \__|      $$ | $$  |                             
   $$ | $$$$$$\  $$\       $$ |$$  / $$$$$$\  $$$$$$$\   $$$$$$\  
   $$ | \____$$\ $$ |      $$$$$  /  \____$$\ $$  __$$\ $$  __$$\ 
   $$ | $$$$$$$ |$$ |      $$  $$<   $$$$$$$ |$$ |  $$ |$$ /  $$ |
   $$ |$$  __$$ |$$ |      $$ |\$$\ $$  __$$ |$$ |  $$ |$$ |  $$ |
   $$ |\$$$$$$$ |$$ |      $$ | \$$\\$$$$$$$ |$$ |  $$ |\$$$$$$$ |
   \__| \_______|\__|      \__|  \__|\_______|\__|  \__| \____$$ |
                                                        $$\   $$ |
                                                        \$$$$$$  |
                                                         \______/ 
```



![1540452648272](C:\Users\w_fancw\Desktop\springboot\assets\1540452648272.png)

## 2.4、测试

![1540452795486](C:\Users\w_fancw\Desktop\springboot\assets\1540452795486.png)

# 3、全局异常处理

```java
import cn.com.yusys.tkbb.constant.Codes;
import cn.com.yusys.tkbb.vo.Json;
import org.apache.shiro.ShiroException;
import org.apache.shiro.authz.UnauthenticatedException;
import org.apache.shiro.authz.UnauthorizedException;
import org.apache.shiro.util.StringUtils;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.web.bind.annotation.ControllerAdvice;
import org.springframework.web.bind.annotation.ExceptionHandler;
import org.springframework.web.bind.annotation.ResponseBody;
import org.springframework.web.servlet.mvc.method.annotation.ResponseEntityExceptionHandler;

/**
 * 统一捕捉异常，返回给前台一个json信息，前台根据这个信息显示对应的提示，或者做页面的跳转。
 */
@ControllerAdvice
public class GlobalExceptionHandler extends ResponseEntityExceptionHandler {


    private static final Logger log = LoggerFactory.getLogger(GlobalExceptionHandler.class);

    //不满足@RequiresGuest注解时抛出的异常信息
    private static final String GUEST_ONLY = "Attempting to perform a guest-only operation";


    @ExceptionHandler(ShiroException.class)
    @ResponseBody
    public Json handleShiroException(ShiroException e) {
        String eName = e.getClass().getSimpleName();
        log.error("shiro执行出错：{}",eName);
        return new Json(eName, false, Codes.SHIRO_ERR, "鉴权或授权过程出错", null);
    }

    @ExceptionHandler(UnauthenticatedException.class)
    @ResponseBody
    public Json page401(UnauthenticatedException e) {
        String eMsg = e.getMessage();
        if (StringUtils.startsWithIgnoreCase(eMsg,GUEST_ONLY)){
            return new Json("Unauthenticated", false, Codes.UNAUTHEN, "只允许游客访问，若您已登录，请先退出登录", null)
                    .data("detail",e.getMessage());
        }else{
            return new Json("Unauthenticated", false, Codes.UNAUTHEN, "用户未登录", null)
                    .data("detail",e.getMessage());
        }
    }

    @ExceptionHandler(UnauthorizedException.class)
    @ResponseBody
    public Json page403() {
        return new Json("Unauthorized", false, Codes.UNAUTHZ, "用户没有访问权限", null);
    }
}
```



# 4、集成shiro

## 4.1、导入starter

![1540452240681](C:\Users\w_fancw\Desktop\springboot\assets\1540452240681.png)

## 4.2、自定义realm

![1540453192936](C:\Users\w_fancw\Desktop\springboot\assets\1540453192936.png)

## 4.3、认证授权跳转

![1540512867415](C:\Users\w_fancw\Desktop\springboot\assets\1540512867415.png)	

### 4.3.1、认证授权控制器

```java
import cn.com.yusys.tkbb.vo.Json;
import org.apache.shiro.authz.UnauthenticatedException;
import org.apache.shiro.authz.UnauthorizedException;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
@RequestMapping("/auth")
public class AuthController {
    private static final Logger log = LoggerFactory.getLogger(AuthController.class);

    /**
     * shiro.loginUrl映射到这里，我在这里直接抛出异常交给GlobalExceptionHandler来统一返回json信息，
     * 您也可以在这里直接返回json，不过这样子就跟GlobalExceptionHandler中返回的json重复了。
     * @return
     */
    @RequestMapping("/401")
    public Json page401() {
        throw new UnauthenticatedException();
    }

    /**
     * shiro.unauthorizedUrl映射到这里。由于约定了url方式只做鉴权控制，不做权限访问控制，
     * 也就是说在ShiroConfig中如果没有做roles[js],perms[mvn:install]这样的权限访问控制配置的话，是不会跳转到这里的。
     * @return
     */
    @RequestMapping("/403")
    public Json page403() {
        throw new UnauthorizedException();
    }

    /**
     * 登录成功跳转到这里，直接返回json。但是实际情况是在login方法中登录成功后返回json了。
     * @return
     */
    @RequestMapping("/index")
    public Json pageIndex() {
        return new Json("index",true,1,"index page",null);
    }
}
```

### 4.3.2、异常代码枚举类

```java
public interface Codes {

    /** 未登录 */
    int UNAUTHEN = 4401;

    /** 未授权，拒绝访问 */
    int UNAUTHZ = 4403;

    /** session超时退出登录 */
    int SESSION_TIMEOUT = 4433;

    /** shiro相关的错误 */
    int SHIRO_ERR = 4444;

    /** 服务端异常 */
    int SERVER_ERR = 5500;

}
```

### 4.3.3、全局异常处理

```java
import cn.com.yusys.tkbb.constant.Codes;
import cn.com.yusys.tkbb.vo.Json;
import org.apache.shiro.ShiroException;
import org.apache.shiro.authz.UnauthenticatedException;
import org.apache.shiro.authz.UnauthorizedException;
import org.apache.shiro.util.StringUtils;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.web.bind.annotation.ControllerAdvice;
import org.springframework.web.bind.annotation.ExceptionHandler;
import org.springframework.web.bind.annotation.ResponseBody;
import org.springframework.web.servlet.mvc.method.annotation.ResponseEntityExceptionHandler;

/**
 * 统一捕捉异常，返回给前台一个json信息，前台根据这个信息显示对应的提示，或者做页面的跳转。
 */
@ControllerAdvice
public class GlobalExceptionHandler extends ResponseEntityExceptionHandler {


    private static final Logger log = LoggerFactory.getLogger(GlobalExceptionHandler.class);

    //不满足@RequiresGuest注解时抛出的异常信息
    private static final String GUEST_ONLY = "Attempting to perform a guest-only operation";


    @ExceptionHandler(ShiroException.class)
    @ResponseBody
    public Json handleShiroException(ShiroException e) {
        String eName = e.getClass().getSimpleName();
        log.error("shiro执行出错：{}",eName);
        return new Json(eName, false, Codes.SHIRO_ERR, "鉴权或授权过程出错", null);
    }

    @ExceptionHandler(UnauthenticatedException.class)
    @ResponseBody
    public Json page401(UnauthenticatedException e) {
        String eMsg = e.getMessage();
        if (StringUtils.startsWithIgnoreCase(eMsg,GUEST_ONLY)){
            return new Json("Unauthenticated", false, Codes.UNAUTHEN, "只允许游客访问，若您已登录，请先退出登录", null)
                    .data("detail",e.getMessage());
        }else{
            return new Json("Unauthenticated", false, Codes.UNAUTHEN, "用户未登录", null)
                    .data("detail",e.getMessage());
        }
    }

    @ExceptionHandler(UnauthorizedException.class)
    @ResponseBody
    public Json page403() {
        return new Json("Unauthorized", false, Codes.UNAUTHZ, "用户没有访问权限", null);
    }
}
```



## 4.4、ShiroConfig

![1540453281119](C:\Users\w_fancw\Desktop\springboot\assets\1540453281119.png)

**ShiroConfig是一个配置类**

### 4.4.1、注入自定义realm

![1540512266520](C:\Users\w_fancw\Desktop\springboot\assets\1540512266520.png)



### 4.4.2、开启内存缓存

![1540512307466](C:\Users\w_fancw\Desktop\springboot\assets\1540512307466.png)



### 4.4.3、配置鉴权filter

![1540512356256](C:\Users\w_fancw\Desktop\springboot\assets\1540512356256.png)

### 4.4.4、配置超时时间

![1540518789115](C:\Users\w_fancw\Desktop\springboot\assets\1540518789115.png)

![1540518805880](C:\Users\w_fancw\Desktop\springboot\assets\1540518805880.png)

![1540518821023](C:\Users\w_fancw\Desktop\springboot\assets\1540518821023.png)



# 5、集成Mybatis+

## 5.1、DB driver

![1540777329664](C:\Users\w_fancw\Desktop\springboot\assets\1540777329664.png)

### 5.1.3、开发环境

![1540520037985](C:\Users\w_fancw\Desktop\springboot\assets\1540520037985.png)

### 5.1.4、生产环境

![1540520137218](C:\Users\w_fancw\Desktop\springboot\assets\1540520137218.png)

**注意：一般开发与生产环境的配置是不一样的**

## 5.2、引入druid

![1540520203463](C:\Users\w_fancw\Desktop\springboot\assets\1540520203463.png)

### 5.3、配置druid

```properties
#druid
spring.datasource.druid.initialSize=5
spring.datasource.druid.minIdle=5
spring.datasource.druid.maxWait=60000
spring.datasource.druid.maxActive=20
spring.datasource.druid.timeBetweenEvictionRunsMillis=60000
spring.datasource.druid.minEvictableIdleTimeMillis=300000
spring.datasource.druid.validationQuery=SELECT 1 from dual
spring.datasource.druid.testWhileIdle=true
spring.datasource.druid.testOnBorrow=false
spring.datasource.druid.testOnReturn=false
spring.datasource.druid.poolPreparedStatements=true
spring.datasource.druid.maxPoolPreparedStatementPerConnectionSize=20
```



![1540520434378](C:\Users\w_fancw\Desktop\springboot\assets\1540520434378.png)

## 5.3、引入MyBatis+

### 5.3.1、配置starter

![1540522270403](C:\Users\w_fancw\Desktop\springboot\assets\1540522270403.png)

### 5.3.2、配置mybatis-plus

![1540541205930](C:\Users\w_fancw\Desktop\springboot\assets\1540541205930.png)

```properties
#mybatis-plus
mybatis-plus.global-config.db-config.db-type=oracle
# 如果是放在src/main/java目录下 classpath:/com/yourpackage/*/mapper/*Mapper.xml
# 如果是放在resource目录 classpath:/mapper/*Mapper.xml
mybatis-plus.mapper-locations=classpath:/mapper/*Mapper.xml
#实体扫描，多个package用逗号或者分号分隔
mybatis-plus.type-aliases-package=cn.com.yusys.tkbb.entity
#主键类型  0:"数据库ID自增", 1:"用户输入ID",2:"全局唯一ID (数字类型唯一ID)", 3:"全局唯一ID UUID";
mybatis-plus.global-config.db-config.id-type=input

#字段策略 0:"忽略判断",1:"非 NULL 判断"),2:"非空判断"
mybatis-plus.global-config.db-config.field-strategy=not_null
#驼峰下划线转换
mybatis-plus.global-config.db-config.column-like=true
#刷新mapper 调试神器
#refresh-mapper=true
#数据库大写下划线转换
#capital-mode=true
# Sequence序列接口实现类配置
#mybatis-plus.configuration.key-generators=[com.baomidou.mybatisplus.extension.incrementer.OracleKeyGenerator]


#配置返回数据库(column下划线命名&&返回java实体是驼峰命名)，自动匹配无需as（没开启这个，SQL需要写as： select user_id as userId）
mybatis-plus.configuration.map-underscore-to-camel-case=true
mybatis-plus.configuration.cache-enabled=false
#配置JdbcTypeForNull, oracle数据库必须配置
mybatis-plus.configuration.jdbc-type-for-null=null

#逻辑删除配置（下面3个配置）
mybatis-plus.global-config.db-config.logic-delete-value=1
mybatis-plus.global-config.db-config.logic-not-delete-value=0
#Deprecated: 3.0开始废除此属性，请使用@Bean的方式注入至Spring容器 MybatisConfiguration
#mybatis-plus.global-config.sql-injector=com.baomidou.mybatisplus.extension.incrementer.OracleKeyGenerator

```

### 5.3.3、CodeGenerator

```java
import com.baomidou.mybatisplus.annotation.DbType;
import com.baomidou.mybatisplus.annotation.IdType;
import com.baomidou.mybatisplus.generator.AutoGenerator;
import com.baomidou.mybatisplus.generator.config.*;
import com.baomidou.mybatisplus.generator.config.rules.NamingStrategy;

// 演示例子，执行 main 方法控制台输入模块表名回车自动生成对应项目目录中
public class CodeGenerator {
    public static void main(String[] args) {
        //1、全局配置
        GlobalConfig globalConfig = new GlobalConfig();
        globalConfig
                .setActiveRecord(false)
                .setEnableCache(false)
                .setOutputDir("D:\\IdeaProjects\\tkbb\\src\\main\\java")
                .setFileOverride(true)
                .setIdType(IdType.INPUT)
                .setServiceName("%sService")
                .setBaseResultMap(true)
                .setBaseColumnList(true)
                .setAuthor("fancw")
                .setOpen(false);
        //2、数据源配置
        DataSourceConfig dataSourceConfig = new DataSourceConfig();
        dataSourceConfig.setUrl("jdbc:oracle:thin:@10.88.158.194:1521:oracle")
                .setDriverName("oracle.jdbc.driver.OracleDriver")
                .setUsername("osi")
                .setPassword("osi")
                .setDbType(DbType.ORACLE);

//        dataSourceConfig.setUrl("jdbc:mysql://localhost:3306/biu?characterEncoding=UTF-8&useSSL=false")
//                .setDriverName("com.mysql.jdbc.Driver")
//                .setUsername("root")
//                .setPassword("gsd88888")
//                .setDbType(DbType.MYSQL);
        //3、策略配置
        StrategyConfig strategyConfig = new StrategyConfig();
        strategyConfig
                .setNaming(NamingStrategy.underline_to_camel)
                .setColumnNaming(NamingStrategy.underline_to_camel)
                .setNaming(NamingStrategy.underline_to_camel)
//                TODO
//                .setInclude("SYS_USER")
                .setTablePrefix("SYS_");

        //4、包名策略配置
        PackageConfig packageConfig = new PackageConfig();
        packageConfig.setParent("cn.com.yusys.tkbb")
                .setMapper("mapper")
                .setService("service")
//                .setController("controller")
                .setEntity("entity")
                .setXml("mapper");

        //5、整合配置
        AutoGenerator autoGenerator = new AutoGenerator();
        autoGenerator.setGlobalConfig(globalConfig)
                .setDataSource(dataSourceConfig)
                .setStrategy(strategyConfig)
                .setPackageInfo(packageConfig);
        //6、执行
        autoGenerator.execute();
    }

}
```

### 5.3.4、MyBatisPlusConfig

```java
import com.baomidou.mybatisplus.extension.plugins.PaginationInterceptor;
import org.mybatis.spring.annotation.MapperScan;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
@MapperScan("cn.com.yusys.tkbb.mapper")
public class MyBatisPlusConfig {

    /*
     * 分页插件，自动识别数据库类型
     * 多租户，请参考官网【插件扩展】
     */
    @Bean
    public PaginationInterceptor paginationInterceptor() {
        return new PaginationInterceptor();
    }
}
```

### 5.3.5、测试

![1540541448393](C:\Users\w_fancw\Desktop\springboot\assets\1540541448393.png)

![1540541469306](C:\Users\w_fancw\Desktop\springboot\assets\1540541469306.png)

![1540541479815](C:\Users\w_fancw\Desktop\springboot\assets\1540541479815.png)

# 6、pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>cn.com.yusys</groupId>
    <artifactId>tkbb</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <packaging>jar</packaging>

    <name>tkbb</name>
    <description>Demo project for Spring Boot</description>

    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.0.4.RELEASE</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>

    <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
        <java.version>1.8</java.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>

        <!-- Apache shiro -->
        <dependency>
            <groupId>org.apache.shiro</groupId>
            <artifactId>shiro-spring-boot-web-starter</artifactId>
            <version>1.4.0-RC2</version>
        </dependency>

        <!-- DB -->
        <!--<groupId>mysql</groupId>-->
		<!--<artifactId>mysql-connector-java</artifactId>-->
		<!--<scope>runtime</scope>-->
		<!--</dependency>-->

        <dependency>
            <groupId>com.oracle</groupId>
            <artifactId>ojdbc14</artifactId>
            <version>10.2.0.4.0</version>
        </dependency>

        <!--引入Druid-->
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid-spring-boot-starter</artifactId>
            <version>1.1.9</version>
        </dependency>
        <dependency>
            <groupId>com.baomidou</groupId>
            <artifactId>mybatis-plus-boot-starter</artifactId>
            <version>3.0.1</version>
        </dependency>

        <dependency>
            <groupId>org.apache.commons</groupId>
            <artifactId>commons-lang3</artifactId>
        </dependency>

        <!--<dependency>-->
            <!--<groupId>org.apache.velocity</groupId>-->
            <!--<artifactId>velocity-engine-core</artifactId>-->
            <!--<version>2.0</version>-->
        <!--</dependency>-->

        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>


</project>

```





















