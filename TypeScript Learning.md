## TypeScript 类型

### 类型

TypeScript 一共有下面 `12` 种类型

|  类型   |       例子        |              描述               |
| :-----: | :---------------: | :-----------------------------: |
| number  |    1, -33, 2.5    |            任意数字             |
| string  | 'hi', "hi", `hi`  |           任意字符串            |
| boolean |    true、false    |      布尔值 true 或 false       |
| 字面量  |      其本身       |  限制变量的值就是该字面量的值   |
|   any   |        \*         |            任意类型             |
| unknown |        \*         |         类型安全的 any          |
|  void   | 空值（undefined） |     没有值（或 undefined）      |
|  never  |      没有值       |          不能是任何值           |
| object  |    {key:value}    |         任意的 JS 对象          |
|  array  |      [1,2,3]      |          任意 JS 数组           |
|  tuple  |       [4,5]       | 元素，TS 新增类型，固定长度数组 |
|  enum   |    enum {A, B}    |       枚举，TS 中新增类型       |

#### number

```typescript
let decimal: number = 6;
let hex: number = 0xf00d;
let binary: number = 0b1010;
let octal: number = 0o744;
let big: bigint = 100n;
```

#### boolean

```typescript
let isDone: Boolean = false;
```

#### string

```typescript
let color: string = "blue";
color = "red";

let fullName: string = `Bob Bobbington`;
let age: number = 37;
let sentence: string = `Hello, my name is ${fullName}. I'll be ${
    age + 1
} years old next month.`;
```

#### any

```typescript
let d: any = 4;
d = "hello";
d = true;
```

#### unknown

```typescript
let notSure: unknown = 4;
notSure = "hello";
```

#### void

```typescript
let unusable: void = undefined;
```

#### never

```typescript
function error(message: string): never {
    throw new Error(message);
}
```

#### object

没啥用

```typescript
let obj: object = {};
```

#### array

```typescript
let list: number[] = [1, 2, 3];
let list: Array<number> = [1, 2, 3];
```

#### tuple

```typescript
let x: [string, number];
x = ["hello", 10];
```

#### enum

```typescript
enum Color {
    Red,
    Green,
    Blue,
}
let c: Color = Color.Green;

enum Color {
    Red = 1,
    Green,
    Blue,
}
let c: Color = Color.Green;

enum Color {
    Red = 1,
    Green = 2,
    Blue = 4,
}
let c: Color = Color.Green;
```

#### interface

使用`interface` (接口) 定义对象

-   定义普通属性

```typescript
interface Person {
    name: string;
    age: number;
}
```

-   定义任意属性

```typescript
interface Person {
    name: string;
    age: number;
    [propName: string]: any;
}
```

```typescript
const person: Person = {
    name: "Tom",
    age: 19,
};
```

> 需要注意的是，一旦定义了任意属性，那么确定属性和可选属性的类型都必须是它的类型的子集

#### 字面量

也可以使用字面量去指定变量的类型，通过字面量可以确定变量的取值范围

```typescript
let color: "red" | "blue" | "black";
let num: 1 | 2 | 3 | 4 | 5;
```

### 自动类型判断

-   TS 拥有自动的类型判断机制
-   当对变量的声明和赋值是同时进行的，TS 编译器会自动判断变量的类型
-   所以如果你的变量的声明和赋值时同时进行的，可以省略掉类型声明

### 类型断言

有些情况下，变量的类型对于我们来说是很明确，但是 TS 编译器却并不清楚，此时，可以通过类型断言来告诉编译器变量的类型，断言有两种形式：

-   第一种

    -   ```typescript
        let someValue: unknown = "this is a string";
        let strLength: number = (someValue as string).length;
        ```

-   第二种

    -   ```typescript
        let someValue: unknown = "this is a string";
        let strLength: number = (<string>someValue).length;
        ```

## TypeScript 编译选项

### 编译单个文件

```bash
tsc fileName -w
```

### 编译整个文件夹

编译整个文件夹需要 ts 配置文件 `tsconfig.json`

```json
{
    // ** 任意路径
    // * 任意文件
    // 包含
    "include": ["./src/**/*"],
    // 排除 默认["node_modules", "bower_components", "jspm_packages"]
    "exclude": ["./hello/*"],
    // 只有编译文件夹中少量的文件才使用 file 选项
    "files": [
        "core.ts",
        "sys.ts",
        "types.ts",
        "scanner.ts",
        "parser.ts",
        "utilities.ts",
        "binder.ts",
        "checker.ts",
        "tsc.ts"
    ],
    // 继承 其他编译配置
    "extends": "./config.json",
    // 保存就编译
    "compileOnSave": true,
    "compilerOptions": {
        "target": "ES5", // 指定编译后的js版本， 默认 es3 es5、es6、es2015...es2020 ESNext ==> 最新版本
        "module": "amd", // "CommonJS", "AMD", "System", "UMD", "ES6", "ES2015", "ES2020", "ESNext", "None".
        "lib": [], // 指定项目中使用的一些库，一般情况下不用动
        "outDir": "./dist", // 指定编译后的路径
        "outFile": "", // 将所有的文件编译为一个 js 文件
        "rootDir": "", // 指定项目根目录

        "allowJs": false, // 是否对js文件进行编译
        "checkJs": false, // 是否检查js是否符合规范

        "removeComments": false, // 是否移除注释
        "outFile": "", // 所有全局作用域中的代码会编译合并到同一个文件 system、amd模块
        "noEmit": false, // 不生成编译的文件
        "noEmitOnError": false, // 当有错误是不生成 编译文件

        "strict": false, // 严格检查的总开关
        "alwaysStrict": false, // 编译后的文件是否使用严格模式
        "noImplicitAny": false, // 不允许隐式 any 类型
        "noImplicitThis": false, // 不允许指向不明的this
        "strictNullChecks": false // 严格检查空值
    }
}
```

### 详细配置选项：

-   include

    -   定义希望被编译文件所在的目录

    -   默认值：["\*\*/\*"]

    -   示例：

        -   ```json
            "include":["src/**/*", "tests/**/*"]
            ```

        -   上述示例中，所有 src 目录和 tests 目录下的文件都会被编译

-   exclude

    -   定义需要排除在外的目录

    -   默认值：["node_modules", "bower_components", "jspm_packages"]

    -   示例：

        -   ```json
            "exclude": ["./src/hello/**/*"]
            ```

        -   上述示例中，src 下 hello 目录下的文件都不会被编译

-   extends

    -   定义被继承的配置文件

    -   示例：

        -   ```json
            "extends": "./configs/base"
            ```

        -   上述示例中，当前配置文件中会自动包含 config 目录下 base.json 中的所有配置信息

-   files

    -   指定被编译文件的列表，只有需要编译的文件少时才会用到

    -   示例：

        -   ```json
            "files": [
                "core.ts",
                "sys.ts",
                "types.ts",
                "scanner.ts",
                "parser.ts",
                "utilities.ts",
                "binder.ts",
                "checker.ts",
                "tsc.ts"
              ]
            ```

        -   列表中的文件都会被 TS 编译器所编译

    -   compilerOptions

        -   编译选项是配置文件中非常重要也比较复杂的配置选项

        -   在 compilerOptions 中包含多个子选项，用来完成对编译的配置

            -   项目选项

                -   target

                    -   设置 ts 代码编译的目标版本

                    -   可选值：

                        -   ES3（默认）、ES5、ES6/ES2015、ES7/ES2016、ES2017、ES2018、ES2019、ES2020、ESNext

                    -   示例：

                        -   ```json
                            "compilerOptions": {
                                "target": "ES6"
                            }
                            ```

                        -   如上设置，我们所编写的 ts 代码将会被编译为 ES6 版本的 js 代码

                -   lib

                    -   指定代码运行时所包含的库（宿主环境）

                    -   可选值：

                        -   ES5、ES6/ES2015、ES7/ES2016、ES2017、ES2018、ES2019、ES2020、ESNext、DOM、WebWorker、ScriptHost ......

                    -   示例：

                        -   ```json
                            "compilerOptions": {
                                "target": "ES6",
                                "lib": ["ES6", "DOM"],
                                "outDir": "dist",
                                "outFile": "dist/aa.js"
                            }
                            ```

                -   module

                    -   设置编译后代码使用的模块化系统

                    -   可选值：

                        -   CommonJS、UMD、AMD、System、ES2020、ESNext、None

                    -   示例：

                        -   ```typescript
                            "compilerOptions": {
                                "module": "CommonJS"
                            }
                            ```

                -   outDir

                    -   编译后文件的所在目录

                    -   默认情况下，编译后的 js 文件会和 ts 文件位于相同的目录，设置 outDir 后可以改变编译后文件的位置

                    -   示例：

                        -   ```json
                            "compilerOptions": {
                                "outDir": "dist"
                            }
                            ```

                        -   设置后编译后的 js 文件将会生成到 dist 目录

                -   outFile

                    -   将所有的文件编译为一个 js 文件

                    -   默认会将所有的编写在全局作用域中的代码合并为一个 js 文件，如果 module 制定了 None、System 或 AMD 则会将模块一起合并到文件之中

                    -   示例：

                        -   ```json
                            "compilerOptions": {
                                "outFile": "dist/app.js"
                            }
                            ```

                -   rootDir

                    -   指定代码的根目录，默认情况下编译后文件的目录结构会以最长的公共目录为根目录，通过 rootDir 可以手动指定根目录

                    -   示例：

                        -   ```json
                            "compilerOptions": {
                                "rootDir": "./src"
                            }
                            ```

                -   allowJs

                    -   是否对 js 文件编译

                -   checkJs

                    -   是否对 js 文件进行检查

                    -   示例：

                        -   ```json
                            "compilerOptions": {
                                "allowJs": true,
                                "checkJs": true
                            }
                            ```

                -   removeComments

                    -   是否删除注释
                    -   默认值：false

                -   noEmit

                    -   不对代码进行编译
                    -   默认值：false

                -   sourceMap

                    -   是否生成 sourceMap
                    -   默认值：false

            -   严格检查

                -   strict
                    -   启用所有的严格检查，默认值为 true，设置后相当于开启了所有的严格检查
                -   alwaysStrict
                    -   总是以严格模式对代码进行编译
                -   noImplicitAny
                    -   禁止隐式的 any 类型
                -   noImplicitThis
                    -   禁止类型不明确的 this
                -   strictBindCallApply
                    -   严格检查 bind、call 和 apply 的参数列表
                -   strictFunctionTypes
                    -   严格检查函数的类型
                -   strictNullChecks
                    -   严格的空值检查
                -   strictPropertyInitialization
                    -   严格检查属性是否初始化

            -   额外检查

                -   noFallthroughCasesInSwitch
                    -   检查 switch 语句包含正确的 break
                -   noImplicitReturns
                    -   检查函数没有隐式的返回值
                -   noUnusedLocals
                    -   检查未使用的局部变量
                -   noUnusedParameters
                    -   检查未使用的参数

            -   高级

                -   allowUnreachableCode
                    -   检查不可达代码
                    -   可选值：
                        -   true，忽略不可达代码
                        -   false，不可达代码将引起错误
                -   noEmitOnError
                    -   有错误的情况下不进行编译
                    -   默认值：false

## Ts 属性修饰符

### public（默认）

> 可以在任意位置访问、修改（默认）

```typescript
class Person {
    public name: string; // 写或什么都不写都是public
    public age: number;

    constructor(name: string, age: number) {
        this.name = name; // 可以在类中修改
        this.age = age;
    }

    sayHello() {
        console.log(`大家好，我是${this.name}`);
    }
}

class Employee extends Person {
    constructor(name: string, age: number) {
        super(name, age);
        this.name = name; //子类中可以修改
    }
}

const p = new Person("孙悟空", 18);
p.name = "猪八戒"; // 可以通过对象修改
```

### protected

> 在子类中可以修改，直接实例化以后，不能修改

```typescript
class Person {
    protected name: string;
    protected age: number;

    constructor(name: string, age: number) {
        this.name = name; // 可以修改
        this.age = age;
    }

    sayHello() {
        console.log(`大家好，我是${this.name}`);
    }
}

class Employee extends Person {
    constructor(name: string, age: number) {
        super(name, age);
        this.name = name; //子类中可以修改
    }
}

const p = new Person("孙悟空", 18);
p.name = "猪八戒"; // 不能修改
```

### private

> 私有属性

```typescript
class Person {
    private name: string;
    private age: number;

    constructor(name: string, age: number) {
        this.name = name; // 可以修改
        this.age = age;
    }

    sayHello() {
        console.log(`大家好，我是${this.name}`);
    }
}

class Employee extends Person {
    constructor(name: string, age: number) {
        super(name, age);
        this.name = name; //子类中不能修改
    }
}

const p = new Person("孙悟空", 18);
p.name = "猪八戒"; // 不能修改
```

## Getter & Setter

-   对于一些不希望被任意修改的属性，可以将其设置为 private
-   直接将其设置为 private 将导致无法再通过对象修改其中的属性
-   我们可以在类中定义一组读取、设置属性的方法，这种对属性读取或设置的属性被称为属性的存取器
-   读取属性的方法叫做 setter 方法，设置属性的方法叫做 getter 方法

-   示例

```typescript
class Person {
    private _name: string;

    constructor(name: string) {
        this._name = name;
    }

    get name() {
        return this._name;
    }

    set name(name: string) {
        this._name = name;
    }
}

const p1 = new Person("孙悟空");
console.log(p1.name); // 通过getter读取name属性
p1.name = "猪八戒"; // 通过setter修改name属性
```

### 静态属性

-   静态属性（方法），也称为类属性。使用静态属性无需创建实例，通过类即可直接使用

-   静态属性（方法）使用 `static` 开头

示例：

```typescript
class Tools {
    static PI = 3.1415926;

    static sum(num1: number, num2: number) {
        return num1 + num2;
    }
}

console.log(Tools.PI);
console.log(Tools.sum(123, 456));
```

-   this

    在类中，使用 this 表示当前对象

## 接口

接口的作用类似于抽象类
不同点在于接口中的所有方法和属性都是没有实值的
换句话说接口中的所有方法都是抽象方法。接口主要负责定义一个类的结构，接口可以去限制一个对象的接口，对象只有包含接口中定义的所有属性和方法时才能匹配接口。同时，可以让一个类去实现接口，实现接口时类中要保护接口中的所有属性。

### 示例（检查对象类型）：

```typescript
interface Person {
    name: string;
    sayHello(): void;
}

function fn(per: Person) {
    per.sayHello();
}

fn({
    name: "孙悟空",
    sayHello() {
        console.log(`Hello, 我是 ${this.name}`);
    },
});
```

### 示例（实现）

```typescript
interface Person {
    name: string;
    sayHello(): void;
}

class Student implements Person {
    constructor(public name: string) {}

    sayHello() {
        console.log("大家好，我是" + this.name);
    }
}
```

## 泛型

定义一个函数或类时，有些情况下无法确定其中要使用的具体类型（返回值、参数、属性的类型不能确定），此时泛型便能够发挥作用。

举个例子：

```typescript
function test(arg: any): any {
    return arg;
}
```

上例中，test 函数有一个参数类型不确定，但是能确定的是其返回值的类型和参数的类型是相同的，由于类型不确定所以参数和返回值均使用了 any，但是很明显这样做是不合适的，首先使用 any 会关闭 TS 的类型检查，其次这样设置也不能体现出参数和返回值是相同的类型

使用泛型：

```typescript
function test<T>(arg: T): T {
    return arg;
}
```

这里的`<T>`就是泛型，T 是我们给这个类型起的名字（不一定非叫 T），设置泛型后即可在函数中使用 T 来表示该类型。所以泛型其实很好理解，就表示某个类型。
那么如何使用上边的函数呢？

-   方式一（直接使用）：

```typescript
test(10);
```

使用时可以直接传递参数使用，类型会由 TS 自动推断出来，但有时编译器无法自动推断时还需要使用下面的方式

-   方式二（指定类型）：

```typescript
test<number>(10);
```

也可以在函数后手动指定泛型，可以同时指定多个泛型，泛型间使用逗号隔开：

```typescript
function test<T, K>(a: T, b: K): K {
    return b;
}
test<number, string>(10, "hello");
```

使用泛型时，完全可以将泛型当成是一个普通的类去使用，类中同样可以使用泛型：

```typescript
class MyClass<T> {
    prop: T;

    constructor(prop: T) {
        this.prop = prop;
    }
}
```

除此之外，也可以对泛型的范围进行约束

```typescript
interface MyInter {
    length: number;
}
function test<T extends MyInter>(arg: T): number {
    return arg.length;
}
```

使用 T extends MyInter 表示泛型 T 必须是 MyInter 的子类，不一定非要使用接口类和抽象类同样适用。
