---
title: Guava CaseFormat
date: 2023-02-19 10:07:46
categories:
- Guava
- CaseFormat
tags:
- Reference

---

#### Guava CaseFormat

不同命名风格的字符串之间的转换

以下每个枚举类代表一种字符串的命名风格

```java
//短分隔线连接字符的方式的字符串，比如:lower-hyphen,first-second
CaseFormat.LOWER_HYPHEN
//短下划线连接字符的方式的字符串，比如: lower_hyphen,first_second 数据库字段常用
CaseFormat.LOWER_UNDERSCORE
//java常用的变量命名方式 驼峰方式 比如: loweHyphen,firstSecond
CaseFormat.LOWER_CAMEL
//java常用类命名方式 驼峰方式但首字母大写 比如: LoweHyphen,FirstSecond
CaseFormat.UPPER_CAMEL
//java 常量风格的字符串 比如: LOWE_HYPHEN,FIRST_SECOND
CaseFormat.UPPER_UNDERSCORE
```

不同风格的字符串之间的转换

```java
		/*String to(CaseFormat format, String str)方法应用，前一个表示字符的风格 后一个表示要转换为的风格*/
		
		//短横线变为下划线
		//输出：first_second
		System.out.println(CaseFormat.LOWER_HYPHEN.to(CaseFormat.LOWER_UNDERSCORE, "first-second"));
		//输出：lower_hyphen
		System.out.println(CaseFormat.LOWER_HYPHEN.to(CaseFormat.LOWER_UNDERSCORE, "lower-hyphen"));
		//输出：lower_hyphen,first_second
		System.out.println(CaseFormat.LOWER_HYPHEN.to(CaseFormat.LOWER_UNDERSCORE, "lower-hyphen,first-second"));
		
		//短横线变为驼峰
		//输出：firstSecond
		System.out.println(CaseFormat.LOWER_HYPHEN.to(CaseFormat.LOWER_CAMEL, "first-second"));
		//输出：lowerHyphen
		System.out.println(CaseFormat.LOWER_HYPHEN.to(CaseFormat.LOWER_CAMEL, "lower-hyphen"));
		//输出：lowerHyphen,firstSecond
		System.out.println(CaseFormat.LOWER_HYPHEN.to(CaseFormat.LOWER_CAMEL, "lower-hyphen,first-second"));
		
		
		/*Converter<String, String> converterTo(CaseFormat targetFormat) 得到一个从当前CaseFormat到目标CaseFormat的Converter*/
		
		Converter<String,String> converter = CaseFormat.LOWER_HYPHEN.converterTo(CaseFormat.LOWER_UNDERSCORE);
		//输出：first_second
		System.out.println(converter.convert("first-second"));
		
		Converter<String,String> converter1 = CaseFormat.LOWER_HYPHEN.converterTo(CaseFormat.LOWER_CAMEL);
		//输出：firstSecond
		System.out.println(converter1.convert("first-second"));
		//输出：first-second
		System.out.println(converter1.reverse().convert("firstSecond"));
```

