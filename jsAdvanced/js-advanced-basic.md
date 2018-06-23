## JS高级

### 图解

![!js高级](!js高级.png)

### ES6

-   概况

    -   开发环境已经普及使用
    -   浏览器环境却支持不好(需要开发环境编译)
    -   内容很多，重点了解常用语法

-   问题

    -   ES6模块化如何使用，开发环境如何打包
    -   Class和普通构造函数有何区别
    -   Promise的基本使用和原理
    -   总结一下ES6的常用功能

-   ES6模块化如何使用，开发环境打包

    -   `import` 和 `export`

        ```javascript
          // util1
          export default {
            a: 100
          }
          // util2
          export function fn1() {
            console.log('fn1');
          }
          export function fn2() {
            console.log('fn2');
          }

          // 使用
          import util1 from './util1.js'
          import {fn1,fn2} from './util2.js'

          console.log(util1);
          fn1();
          fn2();
        ```

    -   开发环境 —— `babel`
        ```shell
          //安装npm模块，编译es6文件
          cnpm i babel-core babel-preset-es2015 babel-preset-latest -D
        ```
    -   开发环境 —— `webpack`（功能强大）
    -   开发环境 —— `rollup`（打包模块化,功能单一）

-   ES6中 `Class`

    -   JS构造函数

        ```javascript
        // 构造函数
        function MathHandle(x, y) {
          this.x = x;
          this.y = y;
        }
        // 原型扩展
        MathHandle.prototype.add = function(x, y) {
          return this.x + this.y;
        }
        // 实例化
        var m = new MathHandle(1, 2);
        console.log(m.add());
        ```

    -   Class基本语法

        ```javascript
        // Class语法
        class MathHandle {
          // 构造器
          constructor(x, y) {
            this.x = x;
            this.y = y;
          }
          add() {
            return this.x + this.y
          }
        }
        const m = new MathHandle(1, 2);
        console.log(m.add());
        ```

    -   语法糖

        ```javascript
        // 本质和构造函数一样
        class MathHandle {
        //
        }
        typeof MathHandle // 'function'
        MathHandle === MathHandle.prototype.constructor // true
        const m = new MathHandle(1,2);
        m.__proto__ === MathHandle.prototype // true
        ```

    -   继承

        ```javascript
        // ES5继承
        // 动物
        function Animal() {
          this.eat = function() {
            console.log('animal eat');
          }
        }
        // 狗
        function Dog() {
          this.bark = function() {
            console.log('dog bark');
          }
        }
        // 继承
        Dog.prototype = new Animal();
        // hashiqi
        var hashiqi = new Dog();
        hashiqi.bark();
        hashiqi.eat();

        
        Dog.prototype.__proto__ === Animal.prototype //true
        // ES6继承
        class Animal {
          constructor(name) {
            this.name = name;
          }
          eat() {
            console.log(`${this.name} eat`);
          }
        }
        class Dog extends Animal {
          constructor(name) {
            super(name);
            this.name = name;
          }
          say() {
            console.log(`${this.name} say`);
          }
        }
        const dog = new Dog('哈士奇');
        dog.say();
        dog.eat();
        ```

        ![!ES5继承](!ES5继承.png)
