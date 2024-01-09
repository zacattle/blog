---
title: 注解：@Profile
date: 2024-01-09 15:01:39
categories:
- Springboot
- 注解
tags:
- Profile
---

## 注解：@Profile

@Profile注解的作用是**指定类或方法**在特定的 Profile 环境生效，任何`@Component`或`@Configuration`注解的类都可以使用`@Profile`注解。在使用DI来依赖注入的时候，能够根据`@profile`标明的环境，将注入符合当前运行环境的相应的bean。

#### `@Prifile`修饰类

```java
@Configuration
@Profile("prod")//特定的配置环境生效，在prod生产环境下生效
public class DataSourceConfig {

    @Bean(destroyMethod="")
    public DataSource dataSource() throws Exception {
        Context ctx = new InitialContext();
        return (DataSource) ctx.lookup("java:comp/env/jdbc/datasource");
    }

}
```

#### `@Profile`修饰方法

不同环境生效不同的DataSource `Bean`

```
@Configuration
public class AppConfig {

    @Bean("dataSource")
    @Profile("dev")
    public DataSource standaloneDataSource() {
        return new EmbeddedDatabaseBuilder()
            .setType(EmbeddedDatabaseType.HSQL)
            .addScript("classpath:com/bank/config/sql/schema.sql")
            .addScript("classpath:com/bank/config/sql/test-data.sql")
            .build();
    }
    
    @Bean("dataSource")
    @Profile("prod")
    public DataSource jndiDataSource() throws Exception {
        Context ctx = new InitialContext();
        return (DataSource) ctx.lookup("java:comp/env/jdbc/datasource");
    }

}
```

#### `@Profile`修饰注解

```
@Target(ElementType.TYPE) 

@Retention(RetentionPolicy.RUNTIME) 

@Profile("prod")

public @interface Production { }
```

之后可以用@Production 代替@Profile("prod")