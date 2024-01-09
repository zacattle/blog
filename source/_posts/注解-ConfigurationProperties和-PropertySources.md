---

title: '注解: @ConfigurationProperties和@PropertySources'
date: 2024-01-09 11:59:55
categories:
- Springboot
- 注解
tags:
- ConfigurationProperties
- PropertySources
---

## @ConfigurationProperties

是springboot中的注解，用于加载配置文件中的配置字段信息，包括

```
application.yml，application-dev.yml,或者application-local.yml
```

中的配置

```
@Configuration
@ConfigurationProperties(prefix = "myapp")
public class MyAppProperties {
    private String name;
    //此处字段上不需要加其他注解，会自动加载配置文件中的 myapp.version信息
    private String version;
    // getters and setters
}

```

上述示例中，`@ConfigurationProperties` 注解将以 `myapp` 前缀开头的属性映射到 `MyAppProperties` 类的字段中，

注意@ConfigurationProperties需要搭配@Configuration或者@Component等注解使用,或者使用@EnableConfigurationProperties指定文件

## @PropertySources

是spring中的注解，用于指定一个或多个属性文件源，与@PropertySource类似，@PropertySource只是加载单个属性文件源，

注意：@PropertySources通常需要搭配@Value或者@ConfigurationProperties一起使用来完成属性的注入

例子：

```java
@Configuration
@PropertySources({@PropertySource(value="classpath:test.properties",encoding="UTF-8")})
public class ConfigerTest {

    @Value("${testName}")
    private String testName;

    public String getTestName() {
        return testName;
    }
    public void setTestName(String testName) {
        this.testName = testName;
    }
}
```

上述示例中，@PropertySources 注解将会在类目录下加载test.properties配置文件中以 `testName` 前缀开头的属性映射到 ConfigerTest 类的testName字段中

```
@Configuration
@PropertySources({@PropertySource(value="classpath:test.properties",encoding="UTF-8")})
@ConfigurationProperties("test")
public class ConfigerTest {

    private String name;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```

上述示例中，@PropertySources 注解将会在类目录下加载test.properties配置文件中以 test.name 的属性映射到 ConfigerTest 类的name字段中

## @PropertySource

同上

# @Value

`@Value`属于`spring`的注解，在`spring-beans`包下，可以在 **字段** 或 **方法参数** 或 **构造函数参数** 上使用，通常用于属性注入。支持`SpEL` (Spring Expression Language)表达式来注入值，同时也支持**属性占位符注入值**

例子：

配置文件 `application.properties`

```java
name=test String
test=${random.value} 
test1=${random.int(10)} 
test2=${test1}ggggg
spring.profiles.active=dev
age=16
debug=true
```

通过@Value获取配置文件中的属性值

```
@RestController
public class ControllerTest {

    @Value("${name}")
    private String name;
    @Value("${test}")
    private String test;
    @Value("${test1}")
    private String test1;
    @Value("${test2}")
    private String test2;
    @Value("${age}")
    private int age;

    @GetMapping("/")
    public Map testMethod(){
        Map dataMap = new HashMap();
        dataMap.put("name",name);
        dataMap.put("test",test);
        dataMap.put("test1",test1);
        dataMap.put("test2",test2);
        dataMap.put("age",age);
        return dataMap;
    }

}
```

## 直接赋值

```java
@Configuration
public class MyConfig {

    @Value("张三")
    private String name;
    
    public String getName() {
        return name;
    }

}
```

### 方法注入

```java
@Configuration
public class MyConfig {

    @Bean
    public Student getName(@Value("${spring.application.name}")String name) {
        Student student = new Student();
        student.setName(name);
        return student;
    }

}
```

