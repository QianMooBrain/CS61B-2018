# Java study

## 第一个java程序 
这是一个示例 

```HelloWorld.java```

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello world!");
    }
}
```
该程序有以下特点:

1. 主程序放在**公共类public class**下面,事实上**==在 Java 中，所有代码都位于类的内部==**

2. ```public class```下面有一个```public main```函数,由前面的关键字可以看出:

​	这个函数声明了**static静态函数**和**void返回类型**

​	同时传递形参为**string[]空数组** 和**args**两个参数

​	由此我们可以窥见java语言的一些特性



**运行该程序**

**终端运行** :

在终端窗口(powershell或git bash)使用cd命令移动到该文件所在目录下  执行如下命令

```bash
$ javac HelloWorld.java
$ java HelloWorld
Hello World! 
```

第一个命令``` javac <FileName>``` 即 java complier ,它负责编译 .java 文件,并生成一个同名的 .class 文件

紧接着 我们运行 ```java ClassName ```命令,这里的**HelloWorld**即程序的主类名,注意不是文件名

在java中我们运行的是程序的主类 

通过这两步便可在终端窗口中运行java程序,如果情况顺利,则会输出写好的字符串

**这是一种原始的编译方式,但这是所有开发端软件编译的底层原理**

![](https://joshhug.gitbooks.io/hug61b/content/assets/compilation_figure.svg)

---

**使用主流编译器运行 :**

![image-20240801165150295](C:\Users\12275\AppData\Roaming\Typora\typora-user-images\image-20240801165150295.png)



## 变量和循环

输出0 - 10 的简单循环程序

```java
public class Main {
    public static void main(String[] args) {
        int x = 0;
        while (x < 10) {
            x = x + 1;
            System.out.print(x + "\n");     //其效果与println相同
        }

    }
}
```

这里我们可以发现java的一些新特性 :

1. 变量的声明必须声明其类型,这与c/c++相似
2. 在print中引用变量不需要指定转换说明,这又区别于c语言

**静态类型static**

当我们尝试在上面代码中加一句错误类型

```java
public class Main {
    public static void main(String[] args) {
        int x = 0;
        while (x < 10) {
            x = x + 1;
            System.out.print(x + "\n");     //其效果与println相同
        }
        x = "horse";	// <--error
    }
}
```

这时的输出结果

> java: incompatible types: java.lang. **String cannot be converted to int**

**String cannot be converted to int** 说明在程序运行之前,java编译器便发现了此错误

与python等动态类型语言相比,java的静态类型使得它不会出现*类型转换错误*



## 类型转换

java中存在与c相同的类型转换

这里引入c的**隐式转换**规则 :

>1、算术运算式中，低类型能够转换为高类型。
>
>​		 例：int + char  +double运算的结果应该为double类型
>
>     2、赋值表达式中，右边表达式的值自动隐式转换为左边变量的类型，并赋值给他。
>
> 		例：int  =  float + char,表达式的右边char 类型和float类型进行运算进行隐式转换为float类型，		在将float类型转换为int类型赋值给表达式左边的int类型变量。
>
>     3、函数调用中参数传递时，系统隐式地将实参转换为形参的类型后，赋给形参。
>
>4、函数有返回值时，系统将隐式地将返回表达式类型转换为返回值类型，赋值给调用函数。

```
int x = 5;
System.out.println(x / 2.0);			//7.0
```

```
int x = 5;
System.out.println(x + 2.3);			//7.3
```

```
int x = 5;
System.out.println(x + "10");			//510
```

如上述三个例子所示