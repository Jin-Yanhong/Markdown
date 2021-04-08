## Java 基础

-   .Java 源文件

```powershell
// 编译
javac *.java
```

-   .class 字节码文件（编译后产生）与 class 类名相同
-   注释方法

```
Java分为单行注释多行注释，初次之外还有文档注释可以被Javadoc解析
```

-   多行注释使用时须注意的点

```
多行注释不可以嵌套
一个文件中可以有多个class，但只能有一个class声明为public，并且需要跟文件名同名
```

-   package 管理
    一个 Something.java 文件它的内容，文件名与 public 修饰的类名相同

```java
package net.java.util;
public class Something{
   ...
}
```

那么它的路径应该是 net/java/util/Something.java 这样保存的。 package(包) 的作用是把不同的 java 程序分类保存，更方便的被其他 java 程序调用。

## 内置数据类型

Java 语言提供了八种基本类型。六种数字类型（四个整数型，两个浮点型），一种字符类型，还有一种布尔型。

### 基本数据类型

#### 数值

##### 整型

-   byte

```
byte 数据类型是8位、有符号的，以二进制补码表示的整数；
最小值是 -128（-2^7）；
最大值是 127（2^7-1）；
默认值是 0；
byte 类型用在大型数组中节约空间，主要代替整数，因为 byte 变量占用的空间只有 int 类型的四分之一；
例子：byte a = 100，byte b = -50。
```

-   short

```
short 数据类型是 16 位、有符号的以二进制补码表示的整数
最小值是 -32768（-2^15）；
最大值是 32767（2^15 - 1）；
Short 数据类型也可以像 byte 那样节省空间。一个short变量是int型变量所占空间的二分之一；
默认值是 0；
例子：short s = 1000，short r = -20000。
```

-   int

```
int 数据类型是32位、有符号的以二进制补码表示的整数；
最小值是 -2,147,483,648（-2^31）；
最大值是 2,147,483,647（2^31 - 1）；
一般地整型变量默认为 int 类型；
默认值是 0 ；
例子：int a = 100000, int b = -200000。
```

-   long

```
long 数据类型是 64 位、有符号的以二进制补码表示的整数；
最小值是 -9,223,372,036,854,775,808（-2^63）；
最大值是 9,223,372,036,854,775,807（2^63 -1）；
这种类型主要使用在需要比较大整数的系统上；
默认值是 0L；
例子： long a = 100000L，Long b = -200000L。
"L"理论上不分大小写，但是若写成"l"容易与数字"1"混淆，不容易分辩。所以最好大写。
```

> 以上四种都是有符号，以二进制补码表示的整数，下面是浮点数

##### 浮点型

-   float

```
float 数据类型是单精度、32位、符合IEEE 754标准的浮点数；
float 在储存大型浮点数组的时候可节省内存空间；
默认值是 0.0f；
浮点数不能用来表示精确的值，如货币；
例子：float f1 = 234.5f。
```

-   double

```
double 数据类型是双精度、64 位、符合IEEE 754标准的浮点数；
浮点数的默认类型为double类型；
double类型同样不能表示精确的值，如货币；
默认值是 0.0d；
例子：double d1 = 123.4。
```

> 通常定义整型变量时用 int

#### 布尔型

#### 字符型

```java
char (1字符 = 2字节 = 16 bit);
char c1 = 'a'; // √
char c2 = 'ab'; // ×
```

> char 类型只能是一个字符，对于多个字符的情况，使用字符串

### 引用数据类型

#### Class （类）

#### 接口

#### 数组

## 数据类型转换

-   自动类型提升

```
低  ------------------------------------>  高
byte,short,char —> int —> long—> float —> double
必须满足 转换前的数据类型的位数 要低于转换后的数据类型
```

-   数据类型转换遵顼的规则

> 不能对 boolean 类型进行类型转换。
>
> 不能把对象类型转换成不相关类的对象。
>
> 在把容量大的类型转换为容量小的类型时必须使用强制类型转换。
>
> 转换过程中可能导致溢出或损失精度，
>
> 浮点数到整数的转换是通过舍弃小数得到，而不是四舍五入

-   java 变量类型

> int a, b, c; // 声明三个 int 型整数：a、 b、c
> int d = 3, e = 4, f = 5; // 声明三个整数并赋予初值
> byte z = 22; // 声明并初始化 z
> String s = "runoob"; // 声明并初始化字符串 s
> double pi = 3.14159; // 声明了双精度浮点型变量 pi
> char x = 'x'; // 声明变量 x 的值是字符 'x'。

-   Java 语言支持的变量类型有：

> 类变量：独立于方法之外的变量，用 static 修饰。
>
> 实例变量：独立于方法之外的变量，不过没有 static 修饰。
>
> 局部变量：类的方法中的变量。

-   局部变量

> 局部变量声明在方法、构造方法或者语句块中；
> 局部变量在方法、构造方法、或者语句块被执行的时候创建，当它们执行完成后，变量将会被销毁；
> 访问修饰符不能用于局部变量；
> 局部变量只在声明它的方法、构造方法或者语句块中可见；

## Java 修饰符

#### 访问控制修饰符

-   **default** (即默认，什么也不写）: 在同一包内可见，不使用任何修饰符。使用对象：类、接口、变量、方法。
-   **private** : 在同一类内可见。使用对象：变量、方法。 **注意：不能修饰类（外部类）**
-   **public** : 对所有类可见。使用对象：类、接口、变量、方法
-   **protected** : 对同一包内的类和所有子类可见。使用对象：变量、方法。 **注意：不能修饰类（外部类）**。
    | 修饰符 | 当前类 | 同一包内 | 子孙类(同一包) | 子孙类(不同包) | 其他包 |
    | :---------- | :----- | :------- | :------------- | :----------------------------------------------------------- | :----- |
    | `public` | Y | Y | Y | Y | Y |
    | `protected` | Y | Y | Y | Y/N（[说明](https://www.runoob.com/java/java-modifier-types.html#protected-desc)） | N |
    | `default` | Y | Y | Y | N | N |
    | `private` | Y | N | N | N | N |

#### 一元运算符

-   **前缀自增自减法(++a,--a):** 先进行自增或者自减运算，再进行表达式运算。
-   **后缀自增自减法(a++,a--):** 先进行表达式运算，再进行自增或者自减运算

```java
public class selfAddMinus{
    public static void main(String[] args){
        int a = 5;//定义一个变量；
        int b = 5;
        int x = 2*++a;
        int y = 2*b++;
        System.out.println("自增运算符前缀运算后a="+a+",x="+x);
        System.out.println("自增运算符后缀运算后b="+b+",y="+y);
    }
}
```

运行结果为

> 自增运算符前缀运算后 a=6，x=12
> 自增运算符后缀运算后 b=6，y=10

-   短路逻辑运算符

> 当使用与逻辑运算符时，在两个操作数都为 true 时，结果才为 true，

## 循环语句

-   Java 增强 for 循环

```java
public class Test {
   public static void main(String args[]){
      int [] numbers = {10, 20, 30, 40, 50};

// 声明新的局部变量，该变量的类型必须和数组元素的类型匹配。其作用域限定在循环语句块，其值与此时数组元素的值相等。
// 表达式：表达式是要访问的数组名，或者是返回值为数组的方法。
      for(int x : numbers ){
         System.out.print( x );
         System.out.print(",");
      }

      System.out.print("\n");
      String [] names ={"James", "Larry", "Tom", "Lacy"};
      for( String name : names ) {
         System.out.print( name );
         System.out.print(",");
      }
   }
}
```

-   continue 语句

> continue 适用于任何循环控制结构中。作用是让程序立刻跳转到下一次循环的迭代。
>
> 在 for 循环中，continue 语句使程序立即跳转到更新语句。
>
> 在 while 或者 do…while 循环中，程序立即跳转到布尔表达式的判断语句。

```java
public class Test {
   public static void main(String args[]) {
      int [] numbers = {10, 20, 30, 40, 50};

      for(int x : numbers ) {
         if( x == 30 ) {
        continue;
         }
         System.out.print( x );
         System.out.print("\n");
      }
   }
}
```

以上实例编译运行结果如下：

> 10
> 20
> 40
> 50

-   switch-case 语句
    如果 case 语句块中没有 break 语句时，JVM 并不会顺序输出每一个 case 对应的返回值，而是继续匹配，匹配不成功则返回默认 case。

```java
public class Test {
   public static void main(String args[]){
      int i = 5;
      switch(i){
         case 0:
            System.out.println("0");
         case 1:
            System.out.println("1");
         case 2:
            System.out.println("2");
         default:
            System.out.println("default");
      }
   }
}
```

以上结果输出为

> default
> 匹配不到 break 继续执行后续的 case，直到匹配到为止

## java 数据类型

-   String
    <font color="red">String 类是不可改变的，所以你一旦创建了 String 对象，那它的值就无法改变了</font>，String 创建的字符串存储在公共池中，而 new 创建的字符串对象在堆上

```java
String s1 = "Runoob";              // String 直接创建
String s2 = "Runoob";              // String 直接创建
String s3 = s1;                    // 相同引用
String s4 = new String("Runoob");   // String 对象创建
String s5 = new String("Runoob");   // String 对象创建
```

-   StringBuffer、StringBuilder 如需要对字符串进行修改，则使用他们
    StringBuilder 类在 Java 5 中被提出，它和 StringBuffer 之间的最大不同在于 StringBuilder 的方法不是线程安全的（不能同步访问）
    <font color="green">由于 StringBuilder 相较于 StringBuffer 有速度优势，所以多数情况下建议使用 StringBuilder 类。</font>
    然而在应用程序要求线程安全的情况下，则必须使用 StringBuffer 类。

## java 修饰符

重点
