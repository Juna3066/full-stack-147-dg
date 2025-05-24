---
{"dg-publish":true,"permalink":"/02-进阶/04-常用-api/","dgPassFrontmatter":true}
---


## 1. Math、System、Runtime


## 2. BigDecimal

```java
double b = 1.0;
double a = 2.0;
double c = a + b;
底层

1/2 +1/4 + 1/8 ... 无限接近 0.3

BigDecimal(double val) // 只能解大数据问题。
BigDecimal(String val) //底层基于字符串。精度、大数据问题都能解决。
BigDecimal.valueOf() //推荐使用。
```

## 3. LocalDate、LocalTime、LocalDateTime
## 4. ZonedId、ZonedDateTime
## 5. Instance
## 6. DateTimeFormater
## 7. Duration、Period

[[02-进阶/03-面向对象编程高级\|上一节：03-面向对象编程高级]]

[[02-进阶/05-常用-api-2\|下一节：05-常用-api-2]]
