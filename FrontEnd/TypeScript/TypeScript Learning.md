## TypeScript 类型

-   联合类型
    ```typescript
    let a: number | string;
    let b: 'male' | 'female'; // 此种方式声明的值不可更改
    ```
-   any 类型 **(Not recommended)**
    ```typescript
    // 不建议使用，在使用过程中会污染其他变量
    let a; // 若只申明变量，不指定类型，不赋值，则默认为any类型
    ```
-   unknown **（这点不同于 any）**
    ```typescript
    // 将已知类型的变量赋值给unknow是错误的，不能直接赋值给其他变量
    let a: string;
    let b: unknown;
    a = b; //error
    // 如果需要可以如下解决;
    if (typeof b === 'string') {
        //...
    }
    ```
-   类型断言
    ```typescript
    // s 的类型是string
    let s: string;
    let e;
    s = e as string;
    s = <string>e;
    ```
-   空值 void
    ```typescript
    // 用来表示空
    function ():void{
    }
    ```
-   never
    ```typescript
    // 用来表示空
    function (): never {
        throw new Error('error');
    }
    ```
-   object

    ```typescript
    let a: object; // 实际不这么使用
    a = {};
    a = function () { }

    let b: { name: string, age?} // 属性名称后边加个 "?" 表示属性可选(属性名称需一一对应)
    b = { name: "孙悟空" }

    //当需要自定义属性时，如下处理
    let c = { name: "string", [propName: string ] : any }
    c = { name: "八戒", gender: 'male', age: 18 } // 此时name属性是必选属性

    let d: (a: number, b: number) => number; // d是一个函数，包含a、b两个类型为number类型的参数
    d = function (n1: number, n2: number): number {
        return n1 + n2
    }
    ```

-   Array
    ```typescript
    // 声明一个数组，数组里面的元素都是string
    let e: string[];
    let e: Array<string>;
    ```
-   tuple 元组
    ```typescript
    // 固定长度的数组，存储的数据类型可以不同
    let h: [string, number];
    let h: ['123', '1234'];
    ```
-   枚举类型

    ```typescript
    // 在多个值之间选择的时候 性别、学历等

    enum Gender {
        Male = 1,
        Female = 0,
    }

    let i: { name: string; gender: Gender };
    i = {
        name: '孙悟空',
        gender: Gender.Male,
    };
    console.log(i.gender === Gender.Male); // 此时Male、Female的值是多少，并不在意

    let j: { name: string } & { age: number };
    j = { name: '孙悟空', age: 1 };
    ```

-   类型的别名
    ```typescript
    type myType = 1 | 2 | 3 | 4 | 5;
    let K: myType;
    let L: myType;
    ```

## TypeScript 编译选项

编译参数

```bash
// 单个文件 监视模式
tsc fileName -w
```

## tsconfig.json

参数说明

```json
{
    // ** 任意路径
    // * 任意文件

    // 包含
    "include": ["./src/**/*"],
    // 排除
    "exclude": ["./hello/*"],
    // 继承 其他编译配置
    "extends": "../config.json",
    // 保存就编译
    "compileOnSave": true,
    "compilerOptions": {
        // 指定编译后的js版本
        "target": "ES3", // 默认  es5、es6、es2015...es2020 ESNext ==> 最新版本
        "module": "amd", // "CommonJS", "AMD", "System", "UMD", "ES6", "ES2015", "ES2020", "ESNext", "None".
        "lib": [], // 指定项目中使用的一些库，一般情况下不用动
        "outDir": "./dist", // 指定编译后的路径
        "outFile": "" // 所有全局作用域中的代码会编译合并到同一个文件 system、amd模块
    }
}
```

-   模块化规范

    -   CommonJS

    ```javascript
    // nodejs 使用
    // 定义
    module.exports = {};
    exports.xxx = 'xxx';
    // 引用
    var math = require('math');
    ```

    -   AMD （Asynchronous Module Definition）异步模块定义

    ```javascript
    require([module], callback);
    eg: require(['math'], function (math) {
        math.add(2, 3);
    });
    ```

    -   ES6

    ```javascript
    // 定义
    export default getArea = (r) => PI * r * r

    // 引用
    import {fun1 ,fun2} from "..."
    import default as getArea from './circle'
    import * as circle from './circle'

    // 或者
    let getArea = (r) => PI * r * r
    export {
        getArea as default
    }

    ```

    除此之外，还有 System，UMD，ES2015，ES2020，ESNext，None 规范

    ```typescript
    let dom = document.querySelectorAll(['name=age']);
    dom?.addEventListener();
    ```

## Ts 修饰符

-   public

    > 可以在任意位置访问、修改（默认）

-   private

    > 私有属性

```json
{
    // ** 任意路径
    // * 任意文件
    // 包含
    "include": ["./src/**/*"],
    // 排除
    "exclude": ["./hello/*"],
    // 继承 其他编译配置
    "extends": "./config.json",
    // 保存就编译
    "compileOnSave": true,
    "compilerOptions": {
        "target": "ES5", // 指定编译后的js版本， 默认  es5、es6、es2015...es2020 ESNext ==> 最新版本
        "module": "amd", // "CommonJS", "AMD", "System", "UMD", "ES6", "ES2015", "ES2020", "ESNext", "None".
        "lib": [], // 指定项目中使用的一些库，一般情况下不用动
        "outDir": "./dist", // 指定编译后的路径

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
