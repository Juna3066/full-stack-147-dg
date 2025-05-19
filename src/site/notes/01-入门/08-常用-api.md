---
{"dg-publish":true,"permalink":"/01-入门/08-常用-api/","dgPassFrontmatter":true}
---


## 1. API

Application programming interface 应用程序编程接口（别人写好的程序，自己可以直接调用）

称自己为，API 调用工程师, 提高了开发效率。

API 文档（应用程序编程接口文档，程序的说明书）

#TODO 

![assets/01-入门/08-常用-api/IMG-20250520-012542-122.png](/img/user/assets/01-%E5%85%A5%E9%97%A8/08-%E5%B8%B8%E7%94%A8-api/IMG-20250520-012542-122.png)


## 2. 包

描述类的位置。语法 `package 包名;` 

例如： `package com.juna;` 类的位置在操作系统实际目录结构 com/juna 文件夹。

导包语法 `import 包名.类名;` 例如：
```Java
import com.jun.*;
import com.bao.Student

//常用包
//java.lang
//java.util
//java.io
//......

```

**注意点：**
- 同一个包下的类可以相互调用，不用导包。
- 调用 java. lang 包下的类，不用导包。
- 调用不同包下的类，需要导包。
- 调用需要导包的类，如果存在同名，只能导入一个包，其余的需要带包访问 `com.blix.Student stu = new Student();`

## 3. String

String 是引用数据类型。

- **不可变字符串对象**：String 字符串对象是不可变对象。对象在内存中的值一旦创建，就不可变。但是，字符串变量对字符串对象的引用是可以改变的。
- Java 程序 `"..."` 写出来的字符串存储在**常量池中**。且相**同字符串只保存一份**。
- Java 程序中 `new` 出来的字符串存**储在堆内存中**。**每次 new** 字符串对象，即使内容相同，也**都会生成新的对象**。

```Java
package com.juna;  
  
public class Demo {  
    public static void main(String[] args) {  
        String a = "app";  //1 常量池 "app"
        String b = "apple";  //2 常量池 “apple”
        String c = "app" + "le";  //和 b 引用同一个常量池字中的字符串对象 
        String d = new String("apple");  //3 堆  
        String e = new String("apple");  //4 堆  
        String f = a + "le";   //5 堆  
  
        //内存中创建了几个字符串对象？5个  
        System.out.println(b == c); // true  
        System.out.println(b == d); // false  
        System.out.println(b == e); // false  
        System.out.println(b == f); // false  
        System.out.println(e == f); // false  
    }  
}
```

### 3.1. 常用 API

```Java

```

### 3.2. 案例

#### 3.2.1. 用户登录

```Java

```

#### 3.2.2. 用 String 开发验证码

```Java

```

## 4. ArrayList

### 4.1. 常用 API

```Java

```

### 4.2. 案例

```Java

```

#### 4.2.1. 从容器找数据并成功删除

```Java

```

#### 4.2.2. 模仿外卖系统的商家系统

```Java

```

[[01-入门/07-面向对象编程基础\|上一节：07-面向对象编程基础]]
[[01-入门/09-demo-atm\|下一节：09-demo-atm]]
