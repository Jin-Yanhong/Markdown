## java 继承

-   格式

```java
class 父类 {
}

class 子类 extends 父类 {
}
```

-   继承类型
    <img src="https://gitee.com/Coder-jin/PicStore/raw/master/java-extends-2020-12-08.png" alt="img"  />
    <font color="orange">需要注意的是 Java 不支持多继承，但支持多重继承。</font>
-   继承的特性
    > -   子类拥有父类非 private 的属性、方法。
    > -   子类可以拥有自己的属性和方法，即子类可以对父类进行扩展。
    > -   子类可以用自己的方式实现父类的方法。
    > -   Java 的继承是单继承，但是可以多重继承，单继承就是一个子类只能继承一个父类，多重继承就是，例如 B 类继承 A 类，C 类继承 B 类，所以按照关系就是 B 类是 C 类的父类，A 类是 B 类的父类，这是 Java 继承区别于 C++ 继承的一个特性。
    > -   提高了类之间的耦合性（继承的缺点，耦合度高就会造成代码之间的联系越紧密，代码独立性越差）
-   继承关键字
    extends 关键字

    > 在 Java 中，类的继承是单一继承，也就是说，一个子类只能拥有一个父类，所以 extends 只能继承一个类。

    implements 关键字

    > 使用 implements 关键字可以变相的使 java 具有多继承的特性，使用范围为类继承接口的情况，可以同时继承多个接口（接口跟接口之间采用逗号分隔）。

    super

    > 我们可以通过 super 关键字来实现对父类成员的访问，用来引用当前对象的父类。

    this

    > 类似于 js 对象

    final

    > 关键字声明类可以把类定义为不能继承的，即最终类；或者用于修饰方法，该方法不能被子类重写

    ```java
    修饰符(public/private/default/protected) final 返回值类型 方法名(){//方法体}
    ```

    <font color="orange">实例变量也可以被定义为 final，被定义为 final 的变量不能被修改。被声明为 final 类的方法自动地声明为 final，但是实例变量并不是 final</font>
