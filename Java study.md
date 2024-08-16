## 面向对象编程(OOP)

**什么是面向对象编程(Object Oriented Programming)**

[什么是面向对象-CSDN博客](https://blog.csdn.net/ThinkWon/article/details/100667386)

- 面向过程编程 : 为解决某一个实际问题开发一个程序,每次都要重新开发
- 面向对象编程 : 把实际问题抽象成对象, 编写然后封装, 用户端只需使用接口即可处理问题

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

> 对于Java Could not find or load main class错误类型
>
> 尝试: **java -cp . HelloWorld** 这一命令
>
> -cp . 指定java在当前目录下查找class文件

**这是一种原始的编译方式,但这是所有开发端软件编译的底层原理**

![](https://joshhug.gitbooks.io/hug61b/content/assets/compilation_figure.svg)

---

**使用主流编译器运行 :**

![image-20240801165150295](C:\Users\12275\AppData\Roaming\Typora\typora-user-images\image-20240801165150295.png)



## 变量(variable)

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

#### 整型

| 整型  | 占用字节空间大小 |       取值范围       | 默认值 |
| :---: | :--------------: | :------------------: | :----: |
| byte  |      1字节       |      -128 ~ 127      |   0    |
| short |      2字节       |    -32768 ~ 32767    |   0    |
|  int  |      4字节       | -2^31 ~ （2^31） - 1 |   0    |
| long  |      8字节       | -2^63 ~ （2^63） - 1 |   0L   |

#### 浮点型

| 浮点型 | 占用字节空间大小 | 取值范围 | 默认值 |
| :----: | :--------------: | :------: | :----: |
| float  |      4字节       |  10^38   |  0.0F  |
| double |      8字节       |  10^308  |  0.0   |

#### 字符型

| 字符型 | 占用字节空间大小 | 取值范围  | 默认值 |
| :----: | :--------------: | :-------: | :----: |
|  char  |      2字节       | 0 ~ 65535 | ‘\u0’  |

char 数据类型可以储存任何字符 ,实际存储方式是整数型,注意字符只能由一个

#### 布尔型

| 布尔型  | 占用字节空间大小 |  取值范围   | 默认值 |
| :-----: | :--------------: | :---------: | :----: |
| boolean |    视情况而定    | true、false | false  |

#### String

string并非基本的数据类型,它属于**引用类型**(像数组)

它是一个类,**声明String类型的变量即创建一个对象**

String类型创建有两种方式

```java
（1）String s1="abc"；                   //s1指向的是String常量池中的字符串

（2）String s2=new String("abc")；       //s2指向的是*堆*上的对象
```

这两种方式在jvm内存中的存储方式不同

**String的默认值为null**

**基本数据类型转字符串**

> 基本数据类型 + " " 即可自动转换





---

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

**自动类型转换**

当变量数据类型与接受的数据类型不一致时,java会尝试进行自动类型转换,其中由**低精度** -> **高精度**的类型转换可以成功,而**高精度**->**低精度**的类型转换会造成可能的数据溢出,**```会被编译器返回警告信息```**,若想强制执行这种转换,则需要使用强制类型转换

**强制类型转换**

在数据前使用括号标记要转换的数据类型

```java
// 左边是int类型，右边是long类型，左右不一样；
// long --> int,范围从大到小；
// 需要强制类型转换。
int num = (int) 100L;
System.out.println(num);//100
```

用char类型数组创建26个字母表

```java
public class Array {
	public static void main(String[] args){

		char[] abcArray = new char[26];
		for(int i = 0; i < abcArray.length; i++){
			abcArray[i] = (char)('A' + i);	//这里'A'+i是int型,因此用强制转换为char型
		}
		for(int j = 0; j < abcArray.length; j++){
			System.out.println(abcArray[j]);
		}
	}
}
```





## 定义函数

定义一个简单的比较函数:

```java
public class Main {
    //自定义函数模块
    public static int larger_function(int a, int b) {
        return a > b ? a : b;
    }

    public static void main(String[] args) {
        System.out.print(larger_function(-5,10));
    }
}
```

在java中,定义函数的关键字是**public static**

由于函数定义在**主类**中,这样的函数被称为**方法(method)**

定义的函数,主函数 都放在**主类**中,且从主函数开始运行,这有点像c语言

**数组形参的传递**

```java
 public static int[] method(int[] x) { // 接收整型数组并返回一个整形数组 其中x是数组名
     
     /*执行模块*/
     
     return x; // 返回数组
 }
```



## 条件语句

```java
int dogSize = 20;
if (dogSize >= 50) {
    System.out.println("woof!");
} 
else if (dogSize >= 10) {
    System.out.println("bark!");
} 
else {
    System.out.println("yip!");
}
```

```java
 switch (month){                           
    case 2:                                        
      days = 28;        
      break;              
    case 4:                                
    case 6:                                          
    case 9:                                            
    case 11:                                                    
      days = 30;            
      break;
    default:
      days = 31;
      break;
}              
```



## 循环语句

while循环

```java
int bottles = 99;
while (bottles > 0) {
    System.out.println(bottles + " bottles of beer on the wall.");
    bottles = bottles - 1;
}
```

for循环

```java
public class ForLoop {
    public static void main(String args[]) {
        int result = 0;
        for (int i = 1; i <= 100; i++) {//1.初始化部分 2.循环条件部分 3.迭代部分
            result += i;//循环体部分
        }
        System.out.println("result=" + result);
    }
}
```



## 输入流 Scanner

**Scannner类**

scannner类是常用的用户输入类,位于```java.util.Scannner```包下面

使用时在主类外面通过```import```导入此包

scanner类常用的输入**方法**有**next()   nextLine()   hasNextxxx()**

**创建一个scanner**

 ```java
Scanner sc=new Scanner(System.in);
 ```

**使用next()方法**

```java
public static void main(String[] args) {
       Scanner sc=new Scanner(System.in);
       System.out.println(sc.next());
       System.out.println(sc.next());
    }
```

第3行 , next()方法阻塞程序并等待用户输入 遇到空格(空字符)读取跳过并结束(与c语言的scanf类似)

第4行 , 第二个next继续读取剩下的字符串(从第一个非空字符开始)

**使用next()接收字符类型输入:**

```java
Scanner scan = new Scanner(System.in);
char s = scan.next().charAt(0);		//接受字符类型输入
```



**使用nextLine()方法**

```java
import java.util.Scanner;

public class Demo2 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("使用nextLine方式接收：");

        if (scanner.hasNextLine()){
            String str = scanner.nextLine();
            System.out.println("输出内容："+str);
        }
        scanner.close();
    }
}
```

nextLine()方法可以**获取带有空字符的字符串**



**使用hasNext()方法**

```java
public static void main(String[] args) {

   	   Scanner sc=new Scanner(System.in);
   	   int i=1;
   	   while(sc.hasNext()){
   	   System.out.println("第"+i+"个字符串"+sc.next());
   	   i++;
        }
   	   System.out.println("输入完成");
	}
```

第5行 , hasNext方法阻塞程序等待用户输入,该方法检测指针指向位置的下一个字符是否为空,非空返回True

​		若为空,则等待用户输入 . **即hasNext永远不会返回False**

在返回True后,程序执行到第6行,next()方法读入字符串,直到第一个空字符结束

一般使用hasNext()检查并限制输入数据的类型

使用**hasNextType()**进行类型限制,此方法只有在类型匹配时返回True,其余返回False

```java
import java.util.Scanner;
 
public class ScannerDemo {
    public static void main(String[] args) {
        Scanner scan = new Scanner(System.in);
        // 从键盘接收数据
        int i = 0;
        float f = 0.0f;
        System.out.print("输入数：");
        if (scan.hasNextInt()) {
            // 判断输入的是否是整数
            i = scan.nextInt();
            // 接收整数
            System.out.println("整数数据：" + i);
        }
        else if (scan.hasNextFloat()) {
            // 判断输入的是否是小数
            f = scan.nextFloat();
            // 接收小数
            System.out.println("小数数据：" + f);
        }
        scan.close();
    }
}
```

此程序演示了一个利用hasNextType()区分不同输入类型.并给出不同的输出的案例





## 数组(array)

### 一维数组 基本介绍

数组是**引用类型**,创建一个数组即创建一个对象

**数组声明**

```java
dataType[] arrayRefVar = new dataType[arraySize];	//新建数组但不填充元素
dataType arrayRefVar[] = new dataType[arraySize];	
实例     
double[] myList = new double[size];
      myList[0] = 5.6;
      myList[1] = 4.5;
      myList[2] = 3.3;
      myList[3] = 13.2;
      myList[4] = 4.0;
      myList[5] = 34.33;
      myList[6] = 34.0;
      myList[7] = 45.45;
      myList[8] = 99.993;
      myList[9] = 11123;
```

**new **命令在内存中为这段数组分配空间 , 使数组名指向具体的内存空间

或

```java
dataType[] arrayRefVar = {value0, value1, ..., valuek};	
```

**length**方法 : 返回数组的长度

```java
array.length
```

**contains**方法 : 查找一个字符串数组中是否含有某一**连续**字符串

```java
stringname.contains(CharSequence chars)
    
如
public class Main {
    public static void main(String[] args) {
        String myStr = "Runoob";
        System.out.println(myStr.contains("Run"));		//true
        System.out.println(myStr.contains("bo"));		//false
        System.out.println(myStr.contains("s"));		//false
    }
}
```



**遍历数组:for-each循环**

不使用下标的情况下遍历数组

```java
for(type element: array)
{
    System.out.println(element);
}
```

```java
public class TestArray {
   public static void main(String[] args) {
      double[] myList = {1.9, 2.9, 3.4, 3.5};
 
      // 打印所有数组元素
      for (double element: myList) {
         System.out.println(element);
      }
   }
}
```



### 数组和引用  (reference)

和c语言相似, java的数组名指向一个确定的地址,由地址访问内存空间

这个数组名是**对一个数组对象**的引用(reference) , 引用类型是一个特殊类型, **不具有具体的数据类型**

与c语言不同的是

> - java**不能**通过地址**直接操作**数组元素,只能通过过下标访问
> - java数组相邻元素地址间的关系不像c语言一样间隔一个数据类型
>- java中数组的地址指向数组的起始位置,每个元素相对于起始位置有一个"偏移量"
> - java的引用不像c的指针可以被一个具体的数据类型(c中的整型)存储并输出

<img src="C:\Users\12275\AppData\Roaming\Typora\typora-user-images\image-20240806183636257.png" alt="image-20240806183636257" style="zoom:50%;" />

**引用类型本身存储一个引用对象的地址(是存储/指向 而不是它本身就是地址)**

> #### gpt4 对于引用的讲解 :
>
> 在Java中，引用本身并没有显式的数据类型。它是一种抽象的概念，用来引用对象或数组，但其具体的实现细节是由Java虚拟机（JVM）管理的。
>
> #### 引用的存储与类型
>
> - **引用类型**:
>   - Java的引用类型包括类类型、接口类型、数组类型等。
>   - 引用类型的变量存储的是对象在内存中的地址，但这个地址是抽象化和封装在JVM内部的，开发者无法直接访问或操作这个地址。
> - **引用的存储**:
>   - 引用通常存储在栈内存（stack memory）中，而引用指向的对象或数组本身存储在堆内存（heap memory）中。
>   - 引用类型变量只占用一个固定大小的内存空间，这个大小通常是32位或64位，具体取决于JVM的实现和目标平台的架构（32位系统或64位系统）。
>
> #### JVM 中的引用实现
>
> - **引用的实现**:
>   - 在JVM中，引用可以被认为是一个包含对象内存地址的指针，但是这个指针是受JVM严格控制的，不能被直接操作。
>   - 引用类型的变量在赋值时，只是复制引用本身，而不是复制对象。这意味着多个引用变量可以指向同一个对象或数组。
> - **引用的类型分类**（JVM层面）:
>   - **强引用**（Strong Reference）: 最常见的引用类型，当一个对象被一个强引用引用时，垃圾回收器不会回收该对象。
>   - **软引用**（Soft Reference）: 允许垃圾回收器在内存不足时回收该对象。
>   - **弱引用**（Weak Reference）: 在垃圾回收时会被立即回收。
>   - **虚引用**（Phantom Reference）: 仅用于跟踪对象的垃圾回收状态，不能通过它访问对象。

### 数组拷贝

**1. for循环拷贝**

**2. Arrays.copyOf()拷贝**





### 例题1 **: ** 数组倒序

```java
public class Test2 {
    public static void main(String[] args){
        int[] test= {1,2,4,5,7};
        for (int i : test) {
            System.out.print(i+" ");
        }
        System.out.println("\n");
        test = Test2.reverse(test);
        for (int i : test) {
            System.out.print(i+" ");
        }
    }
	
//新建一个数组,利用下标把原数组倒序放入新数组
    public static int[] reverse(int[] arr){
        int[] result = new int[arr.length];
        for (int i = 0,j=result.length-1; i < arr.length; i++,j--) {
            result[j] = arr[i];
        }
        return result;
    }
}

```

该方法**空间复杂度**较高,不是最优解法 ↑

```java
/*不使用新数组的方法*/
import java.util.Scanner;

public class ReverseArray {
	public static void main(String[] args) {
		int[] myArray = new int[5];
		Scanner scan = new Scanner(System.in);
		for(int i = 0; i < myArray.length; i++){
			myArray[i] = scan.nextInt();
		}

		int temp = 0;	//记住要初始化
		for(int i = 0; i < myArray.length/2; i++){
			temp = myArray[i];
			myArray[i] = myArray[myArray.length-1-i];
			myArray[myArray.length-1-i] = temp;
		}
		for(int j = 0; j < myArray.length; j++){
			System.out.print(myArray[j] + " ");
		}
		
	}
}
```



### 例题2 : 找出数组最大值

```java
public class Main {
    public static int max(int[] array) {
        int max = array[0];
        int i;
       for (i = 0; i < array.length; i++){
           if(max < array[i]) {
               max = array[i];
           }
       }
        return max;
    }
    public static void main(String[] args) {
        int[] numbers = new int[]{9, 2, 15, 2, 22, 10, 6};
        System.out.print(max(numbers));

    }
}
```



### 例题3 : 找出数组中连续的一段字符串

```java
public class ContinueDemo {
    public static void main(String[] args) {
        String[] a = {"cat", "dog", "laser horse", "ketchup", "horse", "horbse"};

        for (int i = 0; i < a.length; i += 1) {
            if (a[i].contains("horse")) {
                continue;
            }
            for (int j = 0; j < 3; j += 1) {
                System.out.println(a[i]);
            }
        }
    }
}
```



### 例题4 : 数组求和 (难)

> 编写一个函数 `windowPosSum（int[] a， int n）`该函数将每个元素 a[i] 替换为 a[i] 到 a[i + n] 的总和，但前提是 **a[i] 为正值**。
>
> 如果由于我们到达数组的末尾而没有足够的值，我们只对现有值求和。

```java
public class windowpossum {
    public static void main (String[] args){
        int[] array1 = {-1,2,3,4,5,6,7,8,9};
        ranksum(array1);
    }
    public static void ranksum(int[] array){
       int length = array.length;

       for(int i = 0; i < length; i++){
           int sum = 0;         //每次内循环结束重置sum
           for( int j = i ; j < length ; j++){
               if(array[j] >= 0){
                   sum += array[j];
               }
               else continue;		//元素为负时跳出本次求和
           }
           System.out.println(sum);
       }
    }
}

```

### 例题5 : 数组动态扩容(难)

> 要求:
>
> 1. 原始数组使用静态分配 int[] arr = {1, 2, 3}
> 2. 增加的元素放在数组末尾
> 3. 用户可选是否继续增加元素或退出程序

**思路:**

1. 创建新数组,长度为 arr.length+1
2. 拷贝数组
3. 由scanner将扩容元素添加到新数组末尾
4. 销毁原数组 `arr = newarr` (由于原数组无任何引用(无地址)会被JVM自动销毁)
5. 使用循环不断重复,以实现动态扩容(由于至少执行一次故使用do while)

```java
import java.util.Scanner;

public class ExpandArray {
	public static void main(String[] args) {
		int[] arr = {1, 2, 3};
		Scanner scan = new Scanner(System.in);
		
		do{
			int[] newarr = new int[arr.length+1];
			//遍历数组 复制元素
			for(int i = 0; i < arr.length; i++) {
				newarr[i] = arr[i];
			}
			//扩容最后一个元素
			System.out.println("please print an integer");
			newarr[arr.length] = scan.nextInt();
			arr = newarr;
            //重点,原本的arr所占内存空间被销毁,现在arr和newarr指代相同(同时实现了arr+1)
			//输出函数
			System.out.println("====AFTER====");
			for(int i = 0; i < newarr.length; i++) {
				System.out.print(newarr[i] + " ");
			}
			//跳出循环选项
			System.out.println("\nContinue? y or any keys to quit");
			if(scan.next().charAt(0) != 'y') {
				break;
			}

		}
		while(true);

	}
}
```



**扩展 : 数组动态缩减**

与动态扩容思路基本一致

```java
import java.util.Scanner;
public class ReduceArray {
	public static void main(String[] args) {
		int[] arr = {1, 2, 3, 4, 5};
		Scanner scan = new Scanner(System.in);
		
		do{
			int[] newarr = new int[arr.length - 1];
			//遍历数组 复制元素
			for(int i = 0; i < arr.length - 1; i++) {
				newarr[i] = arr[i];
			}
			arr = newarr;

			//输出函数
			System.out.println("====AFTER====");
			for(int i = 0; i < newarr.length; i++) {
				System.out.print(newarr[i] + " ");
			}
			//检查数组剩余元素个数
			if(arr.length == 1) {
				System.out.println("\nthe last one");
				break;
			}
			//跳出循环选项
			System.out.println("\nContinue? y or any keys to quit");
			if(scan.next().charAt(0) != 'y') {
				break;
			}
		}
		while(true);
	}
}
```

### 例题6 : 数组动态增加和动态删减

其实就是例题5的结合 , 但思路略有区别

**核心思路:**

1. 动态增加(见上) , 动态删除(见上)
2. 每次执行完操作后询问用户下一步操作内容(while循环)

```java
import java.util.Scanner;
public class ExpandArray {
	public static void main(String[] args) {
		int[] arr = {1, 2, 3};
		Scanner scan = new Scanner(System.in);
		
		do{
			int[] newarr = new int[arr.length+1];
			//遍历数组 复制元素
			for(int i = 0; i < arr.length; i++) {
				newarr[i] = arr[i];
			}
			//扩容最后一个元素
			System.out.println("\nplease print an integer");
			newarr[arr.length] = scan.nextInt();
			arr = newarr;//重点,原本的arr所占内存空间被销毁,现在arr和newarr指代相同(同时实现了arr+1)
			//输出函数
			System.out.println("====AFTER====");
			for(int i = 0; i < newarr.length; i++) {
				System.out.print(newarr[i] + " ");
			}
			//跳出循环选项
			char key;
			while(true) {
				System.out.println("\nContinue added? y / r to reduce last element / any other keys to quit");
				key = scan.next().charAt(0);
				if( key == 'y' ) {
					break;
				}
				else if( key == 'r') {
					reduce(arr);	//调用reduce函数,传入数组的指针作为参数
				}				
			}
			if(key != 'y' && key != 'r') {
				break;
			}
		}
		while(true);
}
    
		/*动态删除函数*/
		public static void reduce(int[] arr) {
				int[] newarr = new int[arr.length - 1];
				//遍历数组 复制元素
				for(int i = 0; i < arr.length - 1; i++) {
					newarr[i] = arr[i];
				}
				arr = newarr;
				//输出函数
				System.out.println("====AFTER====");
				for(int i = 0; i < newarr.length; i++) {
					System.out.print(newarr[i] + " ");
				}
				//检查数组剩余元素个数
				if(arr.length == 1) {
					System.out.println("\nthe last one");
				}
		}
}
```





### 算法: 冒泡排序

```java
public class BubbleRank {
	public static void main(String[] args){
		int[] arr = {3, 88, 88, 21, 45, 6, 65, 34, 3, 3};
		//start 一个简单的冒泡排序
		int middle = 0;			
		for(int i = 0; i < arr.length - 1; i++){
			for(int j = 0; j < arr.length - i - 1; j++){
				if(arr[j] > arr[j + 1]){
					middle = arr[j];
					arr[j] = arr[j + 1];
					arr[j + 1] = middle;
				}
			}
		}
		//end
		for(int k = 0; k < arr.length; k++){
			System.out.print(arr[k] + " ");
		}
	}
}
```

**思路**

>- 外层循环 `i` 从0遍历到数组的倒数第二个元素。
>- 内层循环 `j` 从0遍历到 `arr.length - i - 1`。
>- 比较 `arr[j]` 和 `arr[j + 1]` 的大小，如果 `arr[j]` 大于 `arr[j + 1]`，则交换两者的位置。
>- **每一轮内层循环结束后，最大的元素都会被放置到数组的末尾位置**，因此不需要再比较已经排好序的部分  `j < arr.length - i - 1`

> 注: 外循环length - 1是为了减少最后一次运算(非必要) , 内循环length - 1是防止数组溢出边界

另一种**伪冒泡循环**:

```java
for(int i = 0; i < arr.length; i++){
			for(int j = i + 1; j < arr.length; j++){
				if(arr[i] > arr[j]){
					middle = arr[j];
					arr[j] = arr[i];
					arr[i] = middle;
				}
			}
		}
```

> **缺点**：
>
> 1. 时间复杂度较高
> 2. 每次比较是从 `i + 1` 开始，效率不高。
> 3. 不能充分利用冒泡排序的特性。



### 算法: 插入排序

**思路**

> 1. 类比扑克牌的插入排序,将目标牌key与之前的每一位array[j]作比较
> 2. 每次比较若array[j] > key 说明目标牌key应该放在比较牌的前面
> 3. 为了给目标牌腾出存放的位置,需要将array[j]右移一位
> 4. 当遇到第一个小于或等于key的牌时,排序结束(不会再遇到比key大的牌),那么key应该放在这个牌的右边,即 array[j + 1] = key ( j + 1是因为while退出之前会多减一位 )

```java
public class InsertArray {
	public static void main(String[] args) {
		int[] arr = {3, 3, 1, 5, 12, 8, 9};
		Insert(arr);
	}

	public static void Insert(int[] array) {
		for(int i = 1; i < array.length; i++) {
			int key = array[i];
			int j = i - 1;
			while(j >= 0 && array[j] > key) {
				array[j + 1] = array[j];  
              //比较第j个元素与key的关系,若array[j]更大,则右移一位为key腾出位置
				j--;
			}
			array[j + 1] = key; //插入key到第一个比key小(或相等)的元素后面
            
			/*每次排序结束后输出当前数组*/
			for(int k = 0; k < array.length; k++) {
				System.out.print(array[k] + " ");
			}
			System.out.print("\n");
		}
	}
}
```

算法过程举例

<img src="C:\Users\12275\AppData\Roaming\Typora\typora-user-images\image-20240808214205076.png" alt="image-20240808214205076" style="zoom:70%;" />



---

### 二维数组

二维数组,即**数组的数组**,二维数组名即**指针的指针**

**声明**

```java
int[][] arr1 = {{0,1,2},
				{2,3,4}
				{4,5}	};	//静态声明

int[][] arr2 = new int[3][3];//动态声明
```

**动态初始化-列数不确定**

```java
int[][] arr3 = new int[3][];//列数不确定,此时一维数组的值为null
//非齐次动态初始化
for(int i = 0; i < arr3.length; i++) {
    arr3[i] = new int[i + 1];	//给每个一维数组分配内存空间, **注意这个+1**
    for(int j = 0; j < arr3[i].length; j++) {
        arr3[i][j] = j;	
    }
}
//输出
for(int i = 0; i < arr.length; i++) {
    for(int j = 0; j < arr3[i].length; j++) {
        System.out.print(arr3[i][j] + " ");
    }
    System.out.print("\n");
}
/* output
0
0 1
0 1 2	*/
```

**二维数组遍历**

```java
public class Twodecimalarr {
	public static void main(String[] args) {
		int[][] arr = new int[3][3];
		for(int i = 0; i < arr.length; i++) {
			for(int j = 0; j < arr[i].length; j++) {
				System.out.print(arr[i][j] + " ");
			}
			System.out.print("\n");
		}
	}
}
/*	输出 output
0 0 0
0 0 0
0 0 0	默认初始化0 */ 
```

**二维数组在内存中的形式**

<img src="https://pic.imgdb.cn/item/66b7792dd9c307b7e926d823.png" style="zoom:67%;"  >

---

**二维数组的声明 易错题**

<img src="https://pic.imgdb.cn/item/66b7784cd9c307b7e9260fc3.png" style="zoom: 67%;">

数组名是一个对数组对象的引用(reference) ,

因此把一个具有确定的数据类型的数组元素赋值数组名(x和y和y[]) 都是非法的

此外, **Java要求赋值操作的左右两边类型要相同或具有兼容性** 因此f选项将二维数组地址赋值给一维数组会造成类型错误



### 例题7 : 杨辉三角

输入任意正整数n,打印n行杨辉三角

**我的基本思路**

> - 二维数组 动态初始化-列数不确定
> - 初始化为1
> - 使用杨辉三角的规律:两肩之和 arr\[i][j] = arr\[i-1][j-1] + arr\[i-1][j];

```java
//基本思路
import java.util.Scanner;
public class YHtriangle {
	public static void main(String[] args) {
		Scanner scan = new Scanner(System.in);
		System.out.print("print an number\n");
		int max = scan.nextInt();

		int[][] arr = new int[max][];

		for(int i = 0; i < arr.length; i++) {
			arr[i] = new int[i + 1]; //为一维数组创建空间
			for(int j = 0; j < arr[i].length; j++) {
				arr[i][j] = 1; //全部初始化为1
			}
		}
		for(int i = 2; i < arr.length; i++) {
			for(int j = 1; j < arr[i].length - 1; j++) {
				arr[i][j] = arr[i-1][j-1] + arr[i-1][j];
			}
		}
		for(int i = 0; i < arr.length; i++) {
			for(int j = 0; j < arr[i].length; j++) {
				System.out.print(arr[i][j] + " ");
			}
			System.out.print("\n");
		}
	}//main end
}
```

**-->改进思路**

> 使用if-else语句,当遇到开头和结尾时初始化为1,其他情况为两肩之和
>
> 改进后的优点:大幅缩减代码量

```java
import java.util.Scanner;
public class YHtriangle {
	public static void main(String[] args) {
		Scanner scan = new Scanner(System.in);
		System.out.print("print an number\n");
     
		int max = scan.nextInt();
		int[][] arr = new int[max][];   //创建一个列数不确定的二维数组
        
		for(int i = 0; i < arr.length; i++) {
			arr[i] = new int[i + 1]; //为一维数组创建空间
			for(int j = 0; j < arr[i].length; j++) {
				if(j == 0 || j == arr[i].length - 1) {
					arr[i][j] = 1;	//每个一维数组的头和尾初始化为1
				}
				else {	//每一行的其余位数为两肩之和(利用杨辉三角的基本性质)
					arr[i][j] = arr[i-1][j-1] + arr[i-1][j];
				}
			} 
		}// for end
		for(int i = 0; i < arr.length; i++) {
			for(int j = 0; j < arr[i].length; j++) {
				System.out.print(arr[i][j] + " ");
			}
			System.out.print("\n");
		}

	}//main end
}
```





## 类与对象

**类(class)**是包含**成员变量/属性(attribute)**和**方法(method)**的自定义数据类型

**对象(object)**是**类(class)**的**实例**

**属性**可以定义为任意类型 , 可以是基本数据类型,也可以是引用类型(数组 , 对象)

**方法**即定义在类里面的函数,调用规则和属性相似

```java
public class DemoClass {
	public static void main(String[] args) {
		Cat newCat = new Cat();	//new一个类的实例
		newCat.sort = "fff"; // 属性赋值
		System.out.print(newCat.sort + "\n"); //属性调用
		Cat.function();	// 方法调用(跨类调用)

	}//main end
}

class Cat {
			String name = "nya";	//利用已有数据类型创建默认属性
			int age = 8;
			String sort;			//创建未初始化的属性,默认值遵循基本规则
			public static void function() {	//创建一个方法
				System.out.println("hello java!!!");
			}
}//class end
```



### 对象在内存中的存储机制

1. 属性的存储机制
   - 字符串(是一个引用,和数组一样) 存放在方法区内
   - 基本数据类型存放在堆空间

<img src="https://pic.imgdb.cn/item/66b77b3ed9c307b7e928d387.png" style="zoom: 50%;">

2. 方法的存储机制

   - 当程序执行到一个方法时,会开辟一个独立的栈空间
   - 当方法执行完毕,将返回值(若果有)返回给 原调用 栈空间
   - 执行完毕的方法其栈空间会被销毁,下次调用会重新创建

   <img src="https://pic.imgdb.cn/item/66b86855d9c307b7e92ebfa9.png" style="zoom: 80%;"  >



### 方法的定义与使用

```java
访问修饰符 返回值类型 方法名(形式参数列表){
    方法体; 
    返回值;
}
```

- 访问修饰符 :

  ​	**private** : 在同一类内可见。使用对象：变量、方法。 注意：不能修饰类（外部类）

  ​	**default** (即缺省，什么也不写，不使用任何关键字）: 在同一包内可见，不使用任何修饰符。使用对象：					类、接口、变量、方法

  ​	**protected** : 对同一包内的类和所有子类可见。使用对象：变量、方法。 注意：不能修饰类（外部类）

  ​	**public** : 对所有类可见。使用对象：类、接口、变量、方法

- 返回值类型 : 可以是基本数据类型和引用类型 , 返回值类型必须与返回值保持一致, 一个方法只能有一						个返回值 (返回多个值则使用数组或对象)

- 形式参数(形参) : 在方法体内使用的参数,在调用时由调用函数传入实际参数(实参). 形参的声明要包含数据类    						型和形参名. 多个形参使用逗号间隔,传入的实参要求数量,顺序和形参保持一致

  > 关于形参 : 基本数据类型传递的是值(值拷贝) 
  >
  > ​				   引用类型传递的是"引用类型"本身 他们指向同一个地址(地址拷贝) 
  >
  > 值拷贝引起的形参变化不会影响到实参;
  >
  > 地址拷贝引起的形参变化会反映到实参上(由地址直接操作实参);

- 方法体 : 函数(方法)的主体部分 , **方法体内不能定义新方法(可以调用已定义的方法)**



**方法调用**

- 同一个类中方法调用 : 直接调用 方法名()
- 跨类方法调用 : 对象名.方法名()  ;  如main()方法调用其他方法就是一种跨类调用
- 跨类调用方法受到访问修饰符影响,如private修饰符仅允许类内调用

### 引用对象的参数传递机制

```java
//有两个对象
class Person {
	String name = "jack";
	int age = 20;
}
class A {
	public static void test(Person p) {
		p = null;
		p = new Person();
	}
}
//在main函数中有:
	Person p = new Person(); //创建一个Person对象
	A.test(p);

// 对象p会发生什么?
```

 首先,main函数中创建了一个名为p的Person类实例. 

接着调用了test()方法并传入形参p(引用类型) ,

 在test()方法中, 该方法先是拷贝传入参数p(同名p),使得它指向对象p的地址`此时的p与main中的p是同名同地址`

接着执行`p=null`语句,使得p引用对象变为'空' `main中的p还是指向p对象地址` `此时的p与main中的p同名不同地址`

下一步`p=new Person()`创建一个新的实例,此时的p有了引用对象,但与main中的对象地址不同

在这个程序中,当`class A`调用完毕后会被jvm销毁,此时test方法中的p被销毁,即该对象没有了对应的引用类型,同样会被jvm销毁

<img src="https://pic.imgdb.cn/item/66b88e1dd9c307b7e9638a20.png" style="zoom: 100%;" >





## 递归(recursion)

**递归的运行机制**

```java
public class Recurtion {
	public static void main(String[] args) {
		recurtion(4);
	}
	public static void recurtion(int n) {
	    if(n > 2) {
	        recurtion(n - 1);
	    }
	    System.out.println("n = " + n);
	} 
}
```

**在栈中的运行机制**

<img src="https://pic.imgdb.cn/item/66b8c84ad9c307b7e9b36e8f.png" style="zoom: 60%; float:left" >

从main()开始执行并创建一个栈空间,每次读取到recurtion()再创建一个栈空间,每个栈空间的数据相互独立

当执行到recurtion(2)时,不再满足if测试条件,因此从recurtion(2)开始执行下一步命令,直到该方法执行结束

在jvm中,**最后被创建的栈空间最先退出** 因此从上到下依次退出,如果有返回值,则从上到下依次返回每一步的值

最后输出的结果是 : 

> n = 2
> n = 3
> n = 4

### 递归使用重要规则

1. 每次递归调用一个方法,均会开辟一个新的独立空间
2. 每个独立空间内的基本数据类型变量相互独立,引用类型变量共享
3. 递归**必须向退出递归的条件逼近**,否则会出现无限递归(StackOverFlowError 栈溢出)
4. 当方法执行完毕或遇到return,返回值遵循**谁调用就返回给谁**,从递归最后一个方法开始依次返回

### 递归思想

1. 确定函数的递归部分到底要干什么

2. 寻找递归条件

3. 以递归的某一层举例计算看是否符合预期

   **递归的基本结构模版**

   ```java
   伪代码如下：
   int f(int n)
   {
   	if(递归结束条件）
   		return ；		//	基线条件;
   	else
   		return 递归;		//递归条件;
   ```

   当达到递归结束条件时 return一个常量(不再调用方法)使得递归程序能够正确退出

   当满足某一条件时 return递归函数 , 使得程序不断递归一直到顶层(栈顶层)

   > 注: 不一定要把递归部分放在return上,如例2的猴子吃桃问题

### 记忆化搜索

记忆化搜索比递归多了什么？

比递归多了一个“备忘录”的功能（加强版的递归）。递归的缺点就是有时会进行大量的重复计算，导致时间复杂度过大。

“备忘录”就是用来存储每次递归的结果，如果在另一个分支中有进行一样的运算，就不需要再进行递归展开了，只要从“备忘录”中将值取出来直接返回即可。

如下图 , 以斐波那契数列为例

<img src="https://i-blog.csdnimg.cn/blog_migrate/2591ca843a733576f657b3e402627b76.png" style="zoom:67%;" >

记忆化搜索**适用于会有大量重复计算的递归问题** 其时间复杂度相比递归有大幅提升

```java
/*记忆化搜索*/ /*以斐波那契数列为例*/
import java.util.Scanner;
public class Feibonachi {
    public static int[] memo;	//定义全局可见数组memo[]
    //主函数
    public static void main(String[] args) {
    	Scanner scan = new Scanner(System.in);
        int n = scan.nextInt();  // 要计算的斐波那契数列位置
        memo = new int[n + 1];  // 初始化缓存数组 注意这个n+1
      	fibonacci(n);
        for(int i = 0; i < memo.length - 1; i++) {
    	System.out.print(memo[i] + " ");
    	}
    }
    // 记忆化递归函数
    public static int fibonacci(int n) {
        if (n <= 1) {
        	memo[n] = n;
            return memo[n];
        }
        // 检查缓存中是否已有计算结果
        if (memo[n] != 0) {
            return memo[n];
        }
        // 递归计算并存储到缓存
        memo[n] = fibonacci(n - 1) + fibonacci(n - 2);
        return memo[n];
    }
}
```

**重点**

> 1. 在创建"备忘录"数组时要声明为**全局变量**
> 2. 数组的长度n+1可以避免后续调用memo[n]时出现越界错误



### 例题1 : 斐波那契数列

斐波那契数列的定义如下：

>  `F(0) = 0`
>
> `F(1) = 1`
>
> 对于 `n >= 2`，`F(n) = F(n-1) + F(n-2)`

使用基本递归解法 : 

```java
public class Feibonachi {
	public static void main(String[] args) {
		Scanner scan = new Scanner(System.in);
		System.out.print("please print an number:\n");
		f(scan.nextInt());
	}

	public static int f(int n) {
		if(n <= 1) {
			return n;
		}
		else {
			int num = f(n - 1) + f(n - 2);
			return num;
		}
	}
}
```

若输出前10项

> 0 1 1 2 3 5 8 13 21 34   // f(0) ~ f(9)

**使用记忆化搜索**

见	记忆化搜索板块



### 例题2 : 猴子吃桃问题

问题描述 :

猴子第一天摘下若干个桃子，当即吃掉一半，还不过瘾，又多吃了一个。第二天早上又吃掉剩下的一半，还是不满足，又多吃了一个。每天如此，到了第10天早上只剩下一个桃子。求第一天共摘了多少桃子，并列出每一天桃子的剩余数量。

> **思路**
>
> 1. 从第一天到第九天,每天的桃子数量=(前一天数量/2)-1
>
> 2. 若递归从 1 -- 10 , 从最顶端(第十天)算起,桃子数量=(今天+1)*2
>
>    把每一天(today)的桃子数量作为返回值,由递归的性质,我们假设已经知道了下一天(nextday)的桃子数量,根据(nextday+1)*2即可求出today的桃子数量,以此类推

```java
public class MonkeyPeach {
	public static void main(String[] args) {
		peach(1);
	}
	public static int peach(int day) {		
		if(day == 10){
			return 1;
		}
		else {
			int nextday = peach(day + 1);	
			int today = (nextday + 1)*2;
			System.out.println("today the peaches are " + today);
			return today;	//把每天的桃子数量作为返回值
		}
	}
}
```



### 例题3 : 老鼠出迷宫(难)

现有一8行7列的迷宫,用递归思想编写能使老鼠走出迷宫的程序

<img src="https://i-blog.csdnimg.cn/blog_migrate/9d57f9c29e4df4b87ae646c308985fb4.png" style="zoom: 25%; float:left" >

**思路**

> 1. 在整个递归程序中,实际上是从终点到起点的反推
> 2. 下一次递归为本次递归提供条件 : 能通过 -> true ; 不能通过 -> false
> 3. 先向右走或先向下走会出现不同的路线

```java
/*老鼠出迷宫问题*/
public class MiGong {
	public static void main(String[] args) {
		int[][] MiGong = CreatMiGong();
		for(int i = 0; i < MiGong.length; i++) {
			for(int j = 0; j < MiGong[i].length; j++) {
				System.out.print(MiGong[i][j] + " ");
			}
			System.out.print("\n");
		}
		Find(MiGong, 1, 1);	// 调用递归函数

		System.out.print("\n\n\n");
		for(int i = 0; i < MiGong.length; i++) {
			for(int j = 0; j < MiGong[i].length; j++) {
				System.out.print(MiGong[i][j] + " ");
			}
			System.out.print("\n");
		}
	}//main end
	/*初始化迷宫*/
	public static int[][] CreatMiGong() {
		int [][] arr = new int[8][7];
		for(int i = 0; i < 7; i++) {
			arr[0][i] = 1;
			arr[7][i] = 1;
		}
		for(int i = 0; i < 8; i++) {
			arr[i][0] = 1;
			arr[i][6] = 1;
		}
		arr[3][1] = 1;
		arr[3][2] = 1;
		return arr;
	}//function end
	/*递归函数*/
	public static boolean Find(int[][] map, int x, int y) {
		if(map[6][5] == 2)
			return true;		//到达终点时,结束递归
		else {
			if(map[x][y] == 0) {	//当前位置能走
				map[x][y] = 2;		//走过的路标记为2

				if(Find(map, x+1, y)) {//递归探测是否有出路
					return true;	//向下找到出路
				}
				else if(Find(map, x, y+1)) {
					return true;	//向右找到出路
				}
				else if(Find(map, x-1, y)) {
					return true;	//向上找到出路
				}
				else if(Find(map, x, y-1)) {
					return true;	//向左找到出路
				}
				else {
					return false;	//找不到出路
				}
		 	}
		 	else 
		 		return false;	//遇到障碍物或标记2
		}
	}
}
```

**过程讲解:**

- 第一步,程序检测此处为0,并标记为2,由下一次递归结果确定向下走可以,因此向下走
- 第二步,步骤如上,程序由下一次递归返回结果:向下走为false,向右走为true,因此向右走
- 剩下步骤基本一致

> 这里最难理解的地方在于当前递归的判断是基于下一次递归的结果,整个程序实际上是先跑到终点,再由终点开始反推,依次确定路径上哪些点应该被标记为2

这是最基础的问题版本,后续还可以出现: 最短路径 / 列出不同路径 等

**关于回溯现象**

若在(2,2)处将迷宫的障碍物增加,此时按照下右左上的策略,老鼠会卡在(2,1)处((1,1)标记为2)

即返回false并结束此栈,进入上一层栈空间

返回到上一层栈,此栈再此进行新的路径探索(当为"上"时返回true)再次回到(1,1),然后按照原策略继续找路

(此时被卡住的(2,1)位置标记为2,不会再走)



### 例题4 : 汉诺塔

[汉诺塔递归问题思路讲解-bilibili](https://www.bilibili.com/video/BV1Zh411y7XB/?spm_id_from=333.337.search-card.all.click&vd_source=98d8086c38b750b0ce152d6d7c45607f) (crtl + 鼠标左键)

**思路**

> 汉诺塔的每层递归可以总结为:
>
> 1. 把前 n-1 层塔移动到B柱
> 2. 把最后一层(第n层)塔移动到C柱
> 3. 把前 n-1 层塔先移到A柱,再移到C柱
>
> 这三步就是一层递归,一直递归到n=2,由此开始依次处理

<img src="https://pic.imgdb.cn/item/66bb6cbad9c307b7e93222cc.png" style="zoom: 80%;" >

汉诺塔的递归树,形象清晰的展现了每层递归情况

```java
public class HanoiTower {
	public static void main(String[] args) {
		tower(5, 'A', 'B', 'C');
	}
	public static void tower(int n, char A, char B, char C) {
		if(n == 1) {	//ABC三个位置分别是起始,中转,目标
			System.out.println(A +" -> "+ C);
            //这里的A和C应该理解为起始柱和目标柱
		}
		else {
			tower(n - 1, A, C, B);	//前n-1个柱由起始柱到中转柱

			System.out.println(A +" -> "+ C);	//最底层移动到目标柱

			tower(n - 1, B, A, C);	//前n-1个柱由中转柱到目标柱
		}
	}

}
```





## 方法重载(overload)

方法重载 是指在同一个类中,存在多个方法名相同,但形参列表不同的方法

最典型的重载 就是 **System.out.println()** ,该方法能够接收不同的数据类型并处理,这就是重载的体现

**重载的好处:**

1. 减轻起名和记名的麻烦,对于功能相似的方法直接用重载实现,方便编写

**重载的使用细节:**

1. 重载的方法名**必须相同**
2. 重载的形参列表**必须不同** , 必须满足以下其一或更多 :
   - 形参**类型**不同 	如: `int sum(int a, int b)` 和  `double sum(double a, int b)`
   - 形参**数量**不同     如: `int sum(int a, int b)` 和 `int sum(int a, int b, int c)`
   - 形参**顺序**不同     如: `double sum(double a, int b)` 和 `double sum(int a, double b)`

3. 与形参的名称**无关**     如: `sum(int a, int b)` 和 `sum(int n1, int n2)` 不能构成重载

4. 与返回类型**无关**       如: `int sum(int a, int b)` 和 `void sum(int a, int b)` 不能构成重载

也就是说,在编写或判断方法重载时,仅关注方法名和形参是否符合要求

   ```java
/*方法重载实例练习*/
import java.util.Scanner;
public class OverloadExercise {
	public static void main(String[] args) {
		Scanner scan = new Scanner(System.in);
		Method.overf(2);
		Method.overf(3, 4);
		Method.overf("ajsda");
		Method.max(2.3, 4.0, 5);
	}// main end
	public class Method {
		/*方法重载*/
		public static int overf(int n1) {
			return n1 * n1;
		}
		public static int overf(int n1, int n2) {
			return n1 * n2;
		}
		public static void overf(String str) {
			System.out.println(str);	
		}
		public static int max(int n1, int n2) {
			int max = n1 > n2 ? n1 : n2;
			System.out.println(" int max = " + max);
			return max;
		}
		public static double max(double n1, double n2, double n3) {
			double max = n1;
			if(n2 > max) 
				max = n2;
			if(n3 > max)
				max = n3;
			System.out.println("double max = " + max);
			return max;
		}
	}// method class end
}
   ```



   

## 可变参数

可变参数 允许你在方法中传递不定数量的参数。可变参数的数据类型用三个点（`...`）表示，放置在方法参数的类型之前。**可变参数实际上是一个数组，允许你传递任意数量的参数值**。

```java
public void methodName(Type... variableName) {
    // 方法体
}
--------------------------------------------
// 如 int类型多个整数求和:
public int sum(int... nums) {
    int sum = 0;
    for(int i = 0; i < nums.length; i++) {	
        sum += nums[i];
    }
    return sum;
}// 由于形参nums实际上是数组,所以遍历数组求和
```

**可变参数 使用细节**

1. 可变参数的实参**可以为0或任意多个**
2. 可变参数的**本质是数组**
3. 可变参数可以和普通参数一起出现,但是可变参数**必须放在形参列表的最后**
4. 一个形参列表中**只能有一个**可变参数





## 变量作用域

### 全局变量&局部变量

**全局变量(成员变量)**

也就是属性,声明在所属类中的变量,具有**默认值**,**作用域是整个类**(可以被类和子类中的方法调用)

生命周期是**从类的创建到销毁**,生命周期较长

**本类的全局变量可以被其它类调用** : 创建类的实例 / 传入对象形参	(见下例)

全局变量可以被访问修饰符修饰

**局部变量**

除了属性之外的其他变量,不具有默认值,即没有初始化不可使用,作用域范围是定义它的代码块内

生命周期是**从代码块的执行到代码块结束**,生命周期较短

局部变量不可被访问修饰符修饰

**[使用细节]**

- 全局变量(属性)和局部变量可以重名,访问时遵循**就近原则**

- 全局变量与全局变量,局部变量与局部变量 之间,不能重名

```java
 class Scope {
	  public static void main(String[] args) {
		Person p = new Person();//创建Person的实例p
		p.print();
		p.println();
		T t1 = new T();//创建T的实例t1
		t1.f1();
		t1.f2(p);
	}
}
/*默认是default*/
class Person {
	String name = "jack";	//成员变量/全局变量

	void print() {
		String name = "tom";
		System.out.println(name);//输出tom
	}
	void println() {
		System.out.println(name);//输出jack
	}
}
 class T {
 	/*访问其他类的变量 方法1*/
 	void f1() {
 		Person per = new Person();//default类对于同包下的所有类都可见
 		System.out.println(per.name);
 	}
 	void f2(Person p) {	// 传入参数是Person的实例
 		System.out.println(p.name);
 	}
 }
```





## 构造器(constructor)

构造器, 又叫构造方法/构造函数,创建在同名类中,构造器用于**初始化被创建的实例** , 其语法与方法类似

```java
[访问修饰符] 构造方法名(形参) {
    ...
}
```

**使用要点:**

1. 构造器/构造方法 名称必须**与所属类名相同**
2. 构造器创建在同名类里面,可以看做是一个特殊的方法
3. 构造器**没有返回值** , 因此也没有返回类型声明
4. 构造器是**对已创建类的实例的初始化**,而不是创建实例
5. 一个类中可以有多个构造器,即构造器重载,使用规范参考 [**方法重载**]
6. 若创建的类中没有构造器,则程序会生成一个[无参构造器/默认构造方法], 即new一个实例时 类名() `如 Person()` , 显示声明的构造器会覆盖无参构造器,若仍想使用,需要自己创建(即重载)
7. 无参构造器也可以自己声明,此时在构造器内设定的值就是创建实例的默认值

```java
public class Constructor {
	public static void main(String[] args) {
		Person p1 = new Person("jackrolin", 20);//使用构造器
		Person p2 = new Person();//使用自定义的无参构造器
		Cat c = new Cat();//使用系统无参构造器/默认构造方法
	}

	public static class Person {
		String name;
		int age;
		/*创建构造器*/
		public Person(String n, int a) {
			name = n;
			age = a;
			System.out.println("Initialized as " + n + " and " + a);
		}
		/*构造器重载*/
		public Person(String n) {
			name = n;
			System.out.println("Initialized as " + n);
		} 
		/*创建无参构造器*/
		public Person() {
			name = "jack";
			age = 18;
		}
	}
	public static class Cat {
		String name;
	}
}
```



## this关键字

对于一个构造器,当形参名称和类的属性名称相同时,会出现什么?

```java
class Account {
    private String name;
    private double balance;
    private String pwd;
    
    //Account类的一个构造器
    public Account(String name, double balance, String pwd) {
        //构造器的实现---初始化对象
        //不用this
        name = name;
        balance = balance;
        pwd = pwd;
    }
    public void showInfo() {
        System.out.println("name:" + name + " " + "balance:" + balance + " " + "pwd:" + pwd);
        return;
    }
}
```

**根据变量作用域原则**,在调用该构造器时,构造器中的'name'和'balance' 'pwd'都会被视为形参名,也就是构造器执行的是局部变量自身赋值. 当构造器调用完毕,局部变量被销毁,此时属性仍没有被初始化,因此会返回其默认值

<img src="https://i-blog.csdnimg.cn/blog_migrate/93e5b74533c8df57fdfb341c566f65a5.png">

---

**使用this关键字可以解决这一问题**

**this关键字官方解释：**

> [Java虚拟机](https://so.csdn.net/so/search?q=Java虚拟机&spm=1001.2101.3001.7020)（JVM）会给**每个对象**分配一个this,来**代表当前对象**,

**说人话解释：**

- this其实可以理解为对象的一个**属性（成员变量）**,但是这个属性是**隐藏的**.即**this相当于对象的一个隐藏属性。**
- 和对象的其他属性一样，在`new`一个新对象的时候，会在**堆内存**为对象分配空间，属性就储存在这份空间中。且该**this属性**的值就是**对象在堆内存中地址**，即this指向该对象（this代表该对象）.

**[重点]综上：this是对象的隐藏属性（本质就是一个普通的成员变量），和其他`non-static`属性一样，在创建对象的时候会为每个新对象分配该对象的专属成员变量（this就是其中一个），this这个成员变量存储在堆内存中，该变量的值是所属对象在堆内存的地址。**

​	即：创建1000个对象，就有1000个this，它们之间相互独立

**[使用细节]**

- **this关键字可以用来区分当前类的属性&局部变量。**
- 使用this时,**this指代的是当前调用的对象 --> 调用谁,this指向谁**
- 使用this关键字可以用来访问本类的实例属性、实例方法、构造器(“实例”指的就是`non-static`修饰 的）
  - 访问本类实例属性：`this.属性`
  - 访问本类实例方法：`this.方法名(参数列表)`
  - 访问本类构造器：`this(参数列表)`

**注意：**`this(参数列表)`来访问本类构造器需要注意以下几点 :

- **只能在构造器中使用`this(参数列表）;`**即在一个构造器中访问本类的另外一个构造器。（**默认构造器行首是`super();`,）。**
- 显示使用`this()`时，默认的`super()`就被覆盖
- `this(参数列表）` 和 `super(参数列表）`在构造器中有且只能存在一个。
- 若在构造器中使用 `this(参数列表）`，则此语句只能**位于构造器第一行**
- 类中的**静态方法`static method`**中**不能使用`this`**

```java
public class Thistest {

	public static void main(String[] args) {
		test t = new test();
		t.f2();
	}
	public static class test {
		String name;
		int age;
		int salary;
		//在无参构造器中调用其他构造器
		test() {
			this("jack", 18, 4000);//必须放在首句
			System.out.println("transfered");

		}//在构造器中使用this
		test(String name, int age, int salary) {
			this.name = name;
			this.age = age;
			this.salary = salary;
		}
        //使用this访问属性
		void f1() {
			System.out.print("name " + this.name);
/*对于一般写法,name实际上是按照就近原则寻找的,如果明确要访问的是属性,应该用this指代*/
		}
		//使用this调用方法f1()
		void f2() {
			this.f1(); 
		}
	}
}
```



## Java包

在Java中，包是一种将类、接口和其他包分组在一起的机制。

包的主要目的是帮助开发者组织代码, 防止命名冲突, 并控制访问级别. Java使用文件系统的目录作为包的物理表示, 每个包对应于一个目录. 每个目录下存放类文件, 不同包名下的类文件名可以重复.

**为什么使用包**

1. **代码组织**：包帮助开发者将功能相关的类和接口组织在一起, 使得代码更加模块化
2. **避免命名冲突**：包为类和函数提供了命名空间, 这样即使在不同的包中有同名的类, 它们也不会冲突
3. **访问控制**：包可以限制类成员的可见性。使用访问修饰符（如public, protected和private），开发者可以控制哪些其他包的代码可以访问当前包中的类成员

**创建包**

在Java中创建包非常简单。你只需在**源文件的顶部**添加一个`package`语句，然后**将源文件放在与包名称对应的目录结构中**  例如：

```java
package com.example.myapp;

public class MyClass {    
    // 类实现
}
```

在这个例子中，`MyClass`类属于`com.example.myapp `包

根据这个包名，源文件应该位于`com/example/myapp` 的目录路径下

**[注意]:** **一个类只能存在于一个包下** , 也就是一个类文件中只能有一个package

**在IDEA中创建包**

<img src="https://pic.imgdb.cn/item/66bdf59cd9c307b7e98e0be8.png" style="zoom:50%;float:left" >
<img src="https://pic.imgdb.cn/item/66bdf649d9c307b7e98ea282.png" style="zoom: 55%;" >

<img src="https://pic.imgdb.cn/item/66bdf654d9c307b7e98ead37.png">

<img src="https://pic.imgdb.cn/item/66bdf84ed9c307b7e9906f7a.png" style="zoom: 67%;" >

com和example文件夹非必须,只创建一个文件夹也能为包

**引入包**

要在Java程序中使用包内的类，可以使用 `import` 语句。例如，要引入上面创建的`MyClass`，可以在另一个包中的Java文件中这样写：

```java
import com.example.myapp.MyClass;

public class Test {
    public static void main(String[] args) {
       	MyClass obj = new MyClass();
        // 使用MyClass
	}
}
```

也可以使用星号（*）来导入一个包中的所有类：

```java
import com.example.myapp.*;
```

这样，`com.example.myapp`包中的所有类都可以在当前文件中直接使用

在实际开发中, 最好是**只导入需要使用的类**

**引入不同包的同名类文件**

第一个类可以使用 `import com.example.myapp.MyClass;` 写法, 在创建实例的时候 `类名 + 实例名`

第二个类的引入不能再使用上述语句, 而是在创建实例时 `包名.类名 + 实例名 `

```java
import com.example.myapp.MyClass;

public class demo {
    public static void main(String[] args) {
        MyClass mc = new MyClass(); //引入并使用其他包的类
    }
    com.demo.MyClass mc = new com.demo.MyClass();//引入同名不同包的类
}
```

<img src="https://pic.imgdb.cn/item/66bdfc33d9c307b7e9946e78.png"  >

**包命名规范**

通常，包命使用小写英文字母进行命名，并使用“.”进行分割，每个被分割的单元只能包含一个名词。

一般地，包命名常采用顶级域名作为前缀，例如com，net，org，edu，gov，cn，io等，随后紧跟公司/组织/个人名称以及功能模块名称。

**包命名规则**

- 只能以字母作为开头,数字不能放在开头    如: demo.12aa.exc

- 可以包含数字, 字母, 下划线   

- 不能是关键字或保留字    如: demo.class.exe

- 使用小圆点" . " 分割不同的目录层级

  

## 访问修饰符

访问修饰符 :

​	**private** : 在同一类内可见。使用对象：变量、方法。

​					 注意：不能修饰类（外部类）

​	**default** : (即缺省，什么也不写，不使用任何关键字)在同一包内可见，不使用任何修饰符。

​					使用对象: 类、接口、变量、方法

​	**protected** : 对同一包内的类和所有子类可见。使用对象：变量、方法。 

​						注意：不能修饰类（外部类）

​	**public** : 对所有类可见。使用对象：类、接口、变量、方法



<img src="https://i-blog.csdnimg.cn/blog_migrate/7da4ff7952b16683dbc146d4cdc9cb19.png" alt="访问修饰符" style="zoom:120%;" />

这四种访问修饰符均可以修饰 属性attribute 和 方法method

但**只有public和default可以修饰 类class**



## Java三大特性

### 封装

封装（encapsulation）是指对于某个对象，Java隐藏对象的属性和实现细节，**仅对外公开接口，控制在程序中属性的读取和修改的访问级别。**

在Java中每一个类都是一个**类文件** , 功能相似的类文件放在同一个目录下就是**包**,在主类下调用某个类文件时, 只需要导入包名和类名,即可调用, 封装的特性使得代码模块化程度提高

调用封装的类文件时,我们通常不会直接调用/更改其属性(这些属性或方法通常被设为私有private),而是通过类文件提供的公共public方法去间接操作属性, 这种方式更加人性化, 也避免因误修改属性导致程序错误

**创建一个封装**

```java
package 包名;
```

封装必须放在类文件的开头(所有类之上)

**导入封装类**

```java
import 包名.类名;
```

**实例:**

```java
/*封装类Person*/
package com.eli.cc;

public class Person {
    public String name;
    //名字和工资赋予私有属性,不能通过外部方法操作
    private int age;
    private int salary;
	//创建一个默认初始化构造器
    public Person() { 
        this("未初始化", 0, 0);
    }
    /*在构造器中调用set方法*/
    public Person(String name, int age, int salary) {
        this.setName(name);
        this.setAge(age);
        this.setSalary(salary);
    }
    //设置对外开放的方法供给用户端操作
    public void setName(String name) {
       if(name.length() > 1 && name.length() < 7) {
           this.name = name;
       } else {
           System.out.println("illegal name");
       }
    }
    public String getName() {
        return name;
    }
    public void setAge(int age) {
        if(age > 0 && age < 100) {
            this.age = age;
        } else {
            System.out.println("illegal age");
        }
    }
    public int getAge() {
        return age;
    }
    public void setSalary(int salary) {
        this.salary = salary;
    }
    public int getSalary() {
        return salary;
    }
    public void get_info() {
        System.out.println("成员信息如下:");
        System.out.println(this.getName());
        System.out.println(this.getAge());
        System.out.println(this.getSalary());
    }
}
```

对封装类进行操作 :

在这一操作中,我们只能使用封装类提供的"接口"(三个set方法或构造器),若直接对实例的属性进行操作,则会根据提示错误

```java
package com.eli;

/*Person是封装的类,这个主类相当于用户端,
通过指定的方法对封装类进行操作,而非直接修改封装类的属性*/

import com.eli.cc.Person;//导入Person封装类
public class fengzhuang {
    public static void main(String[] args) {
        Person person = new Person();
    //或 Person person = new Person("jack", 20, 10000);
        person.setName("jack");
        person.setAge(20);
        person.setSalary(10000);

        person.get_info();
    }
}
```





### 继承

继承是从已有的类中派生出新的类，新的类能吸收已有类的数据属性和行为，并能扩展新的能力。

在Java之中，如果要实现继承的关系，可以使用如下的语法：

```
class 子类 extends 父类 {
	...//添加子类自己的属性和方法
}
```

子类又被称为派生类； 父类又被称为超类(Super Class)

**[使用细节]**

- **在创建子类实例时, 必须调用父类的构造器, 完成父类的属性初始化, 接着再初始化子类实例**
  - 子类在默认情况下调用父类的无参构造器(显示或隐式), 相当于有一个隐式的 `super()`
  - 如果父类没有无参构造器, 则必须在子类构造器中使用 `super(形参列表)` 指定使用父类的哪个构造器
  - 如果希望显示调用某个父类构造器, 也可以使用 `super(形参列表)`
  - `super()` 放在子类构造器的第一行 
  -  `this(参数列表）` 和 `super(参数列表）`在构造器中有且只能存在一个
- 对父类构造器的调用不限于直接父类, 会一直向上追溯到Object类(顶级父类)
- Java中的所有类都是Object类(顶级父类)的子类
- **一个子类只能继承自一个父类(直接父类)  **[单继承机制]
- 慎用继承, 只有当两个对象是确切的包含与被包含关系时才需要使用



**创建一个Students父类**

```java
/*构造一个父类*/
public class Students {
    private String name;
    private int age;
    private int grades;
    //构造器
    public Students() {
    }
    public Students(String name, int age, int grades) {
        this.setName(name);
        this.setAge(age);
        this.setGrades(grades);
    }
    //接口方法
    public void setName(String name) {
        this.name = name;
    }
    public String getName() {
        return name;
    }
    public void setAge(int age) {
        this.age = age;
    }
    public int getAge() {
        return age;
    }
    public void setGrades(int grades) {
        this.grades = grades;
    }
    public int getGrades() {
        return grades;
    }
    public void showInfo() {
        System.out.println("Name: " + this.getName());
        System.out.println("Age: " + this.getAge());
        System.out.println("Grade: " + this.getGrades());
    }
}
```

**Graduate子类**

```java
/*Graduate类继承了Student类的属性和方法*/
public class Graduate extends Students {
    //Graduate类独有的属性和方法
    private double GPA;
	//创建子类的构造器,其中要包含继承自父类的属性形参
    public Graduate(String name, int age, int grades, double GPA) {
    //**super()将子类构造器的形参传递给父类,使父类初始化**
        super(name, age, grades);
        this.setGPA(GPA);
    }
    public void setGPA(double GPA) {
        if(GPA > 0 && GPA <= 4.0)
        this.GPA = GPA;
        else {
            System.out.println("ileagl gpa");
        }
    }
    public double getGPA() {
        return GPA;
    }
    //重写同名父类方法,这会覆盖父类原有的方法
    public void showInfo() {
        System.out.println("Name: " + this.getName());
        System.out.println("Age: " + this.getAge());
        System.out.println("Grade: " + this.getGrades());
        System.out.println("GPA: " + this.getGPA());
    }
}
```

**在主类中调用**

```java
public class Mainprogramme {
    public static void main(String[] args) {
        //创建Graduate子类的实例,并初始化
        Graduate graduate = new Graduate("Jack Rolin", 20, 98, 4.0);
        graduate.showInfo();
    }
}
```

