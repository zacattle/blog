---
title: Springboot Test
date: 2024-01-09 19:26:22
categories:
- Springboot
- Test
tags:
- Springboot test
---

## Springboot Test

## 注解

### @ContextConfiguration

@ContextConfiguration指定ApplicationContext的配置信息

```java
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration(locations = { "classpath:applicationContext.xml" })//加载配置文件一或多
public class UserServiceTest {
   // TODO
}
```

```java
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration(classes = AppConfig.class)//加载配置类
public class UserServiceTest {
   // TODO
}
```

### @RunWith

@RunWith是一个注解在JUnit测试类上的，它用于指定运行测试类时所使用的测试运行器

常用容器配置

- @RunWith 就是一个运行器
- @RunWith(**JUnit4.class**) 就是指用JUnit4来运行
- @RunWith(**SpringJUnit4ClassRunner.class**),让测试运行于Spring测试环境
- @RunWith(**SpringRunner.class**)：继承了 @RunWith(SpringJUnit4ClassRunner.class)，用法相同，名字简短而已
- @RunWith(**Suite.class**) 的话就是一套测试集合