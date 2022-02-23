# Calss 类

### 类的方法和属性

```typescript
class Dog {
    readonly name: string = '旺财'; // 此处使用 "="
    static readonly age: number = 2; // 此处使用 "="
    static bark() {
        console.log('汪汪汪');
    }
    constructor(name: string, age: number) {
        // 在实例方法中 this => 当前实例
        // 在构造函数中 this => 当前对象就是新建对象
        // 可以通过 this 项新建的对象中添加属性
        this.name = '旺财';
        // this.age = 2; // 静态属性不可改变
        console.log(this);
    }
}
/**
 * 属性
 * 直接定义的属性是实例属性，需要通过对象的实例去访问，
 *      const person = new Person();
 *      person.name
 * 使用 static 关键字定义类属性(静态属性) => 不需要创建对象就可以用的属性
 *      Person.age
 * 方法
 * 直接定义的属性是实例属性，需要通过对象的实例去访问，
 * 使用 static 定义的方法属于实例方法，可以直接访问
 */
```

### 类的继承和方法的重写

```javascript
class Animal {
    name: string;
    age: number;
    constructor(name: string, age: number) {
        this.name = name;
        this.age = age;
    }
    bark() {
        console.log('动物在叫');
    }
}
/**
 * Dog extends Animal
 * Animal => 父类
 * Dog => 子类
 */
// Dog 继承 Animal 的所有属性、方法
/* 开发的时候不要动别人定义好的类，以免出问题 */
class Dog extends Animal {
    // 如果在子类中添加父类中已有的方法，则会覆盖掉父类的方法。父类的方法还在，
    bark() {
        console.log('汪汪汪');
    }
    run() {
        console.log(`${this.name}再跑`);
    }
}
class Cat extends Animal {
    run() {
        console.log(`${this.name}再跑`);
    }
}
// 创建实例
const dog = new Dog('旺财', 2);
const cat = new Cat('喵喵', 2);
dog.run(); // 动物再跑
dog.bark(); // 汪汪汪
cat.bark(); // 汪汪汪
```

### 构造函数的调用

```typescript
// abstract 创建的类 抽象类 区别在于 抽象类 专门用于被继承，本身不能用于创建对象，
abstract class Animals {
    name: string;
    constructor(name: string) {
        this.name = name;
    }
    sayHello() {
        console.log('动物在叫~');
    }
}
class Dog extends Animals {
    age: number;
    // 如果在子类中写了构造函数，在子类构造函数中必须对父类的构造函数进行调用
    constructor(name: string, age: number) {
        super(name); // 这里需要写入 父类 的参数,此处调用super，就相当于调用父类的构造函数
        this.age = age;
        console.log(`我${age}岁了`);
    }
    sayHello() {
        //  在类的方法中， super 就表示当前类的父类
        super.sayHello(); // super 表示父类
    }
}
const dog = new Dog('wangcai', 2);
dog.sayHello();
// super相当于父类，在子类的构造函数中必须调用父类的构造函数，super([...arg]:<type>)
```

### 抽象方法抽象类

```typescript
// abstract 创建的类 抽象类 区别在于 抽象类 专门用于被继承，本身不能用于创建对象，
abstract class Animals {
    name: string;
    constructor(name: string) {
        this.name = name;
    }
    abstract sayHello(): void;
}
class Dog extends Animals {
    age: number;
    // 如果在子类中写了构造函数，在子类构造函数中必须对父类的构造函数进行调用
    constructor(name: string, age: number) {
        super(name); // 这里需要写入 父类 的参数
        this.age = age;
    }
    // 子类继承抽象类后，需要对抽象类的抽象方法经行重写
    sayHello() {
        console.log('汪汪汪');
    }
}
const dog = new Dog('wangcai', 2);
dog.sayHello();
```

### 接口

```typescript
// 描述一个 对象 的类型
// 类型 不能重复声明
type myType = {
    name: string;
    age: number;
};
const obj: myType = {
    name: '小明',
    age: 13,
};
// type myType = {
// }
// 接口用来定义一个 类结构，用来定义一个 类 中应该包含的 属性 和 方法
// 同时接口也可当成类型声明去使用
// 接口可以重复声明
interface myInterrface {
    name: string;
    age: number;
}
interface myInterrface {
    gender: string;
}
const obj2: myInterrface = {
    name: '小明',
    age: 13,
    gender: '男',
};
```

### 接口和类的区分

```typescript
// 描述一个 对象 的类型
// 类型 不能重复声明
type myType = {
    name: string;
    age: number;
};
const obj: myType = {
    name: '小明',
    age: 13,
};
// type myType = {
// }
// 接口用来定义一个 类结构，用来定义一个 类 中应该包含的 属性 和 方法
// 同时接口也可当成类型声明去使用
// 接口可以重复声明
// 接口只定义对象的结构，而不考虑实际的值
// 在接口中定义的方法都是抽象方法
// 定义 类 时，可以使 类 去实现一个接口
// 定义 接口 就是使 类 满足 接口 的的要求，接口就是对类的限制
interface myInterrface {
    name: string;
    age: number;
}
interface myInterrface {
    gender: string;
}
const obj2: myInterrface = {
    name: '小明',
    age: 13,
    gender: '男',
};
interface myInterfaceTwo {
    name: string;
    sayHello(): void;
}
class myclass implements myInterfaceTwo {
    name: string;
    constructor(name: string) {
        this.name = name;
    }
    sayHello(): void {
        console.log('hello');
    }
}
```
