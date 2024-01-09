---
title: springboot指定运行环境
date: 2024-01-09 13:57:17
tags:
- idea
- springboot
---

## Idea中运行springboot程序指定运行环境

两种方式：

通过系统属性 `-D` 和命令行参数 `--` 来设置

### 使用 -D 设置系统属性

使用 -D 参数可以在 Java 虚拟机启动时设置系统属性，从而影响应用程序的运行。在 Spring Boot 应用程序中，可以使用 -D 参数来设置 spring.profiles.active 系统属性，以指定应用程序要使用的配置文件。

例如，要在开发环境中运行应用程序，可以在命令行中使用以下命令：

```java
java -Dspring.profiles.active=dev -jar myapp.jar
```

在上述示例中，我们使用 -D 参数设置了名为 spring.profiles.active 的系统环境属性，将其设置

为 dev，这将指示 Spring Boot 应用程序使用名为 application-dev.properties 或 application-dev.yml 的配置文件。

需要注意的是，使用 -D 参数设置系统属性的方式可以用于**任何 Java 应用程序**（idea中相当于设置VM选项参数），并且可以设置任何系统属性，而不仅仅是 Spring Boot 应用程序的配置文件。

### 使用 -- 设置命令行参数

使用 -- 参数可以在命令行中设置应用程序的命令行参数，从而影响应用程序的运行。在 Spring Boot 应用程序中，可以使用 --spring.profiles.active 参数来指定应用程序要使用的配置文件。

例如，要在开发环境中运行应用程序，可以在命令行中使用以下命令：

```java
java -jar myapp.jar --spring.profiles.active=dev
```


在上述示例中，我们使用 --spring.profiles.active 参数指定要使用的配置文件为 application-dev.properties 或 application-dev.yml。

需要注意的是，使用 -- 参数设置命令行参数的方式是 **Spring Boot 特有的**（idea中相当于设置程序实参），只能用于设置 Spring Boot 应用程序的配置文件。

差异
使用 -D 参数设置系统属性和使用 -- 参数设置命令行参数之间的主要差异在于，使用 -D 参数设置系统属性可以用于任何 Java 应用程序，并且可以设置任何系统属性，而使用 -- 参数设置命令行参数的方式是 Spring Boot 特有的，只能用于设置 Spring Boot 应用程序的配置文件。

此外，使用 -D 参数设置系统属性时，需要将属性名和属性值用等号 = 连接起来，而使用 -- 参数设置命令行参数时，则需要在属性名前加上 -- 前缀。

总结
使用 -D 参数设置系统属性和使用 -- 参数设置命令行参数都是设置 Spring Boot 应用程序的配置文件的有效方法。你可以根据实际需要选择其中一种方式来设置环境变量。需要注意的是，使用 -D 参数设置的系统属性可以在程序运行时动态改变，而使用 -- 参数设置的命令行参数则不能动态改变。

推荐
在Spring-Boot 项目启动时，推荐使用 -- ,如 --spring.profiles.active=dev

