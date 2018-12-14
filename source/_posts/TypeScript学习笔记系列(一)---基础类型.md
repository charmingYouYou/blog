---
title: TypeScript学习笔记系列(一)---基础类型
date: 2018/12/14 17:15:15
auth: charmingYouYou
categories: 
- typescript
tags: 
- typeScript
- 类型检测
---

> `typeScript`是`javascript`的类型的超集, 它可以编译成纯`javascript`
>
> `typescript`可以在任何浏览器、任何计算机和任何操作系统上运行, 并且是开源的

## 初始准备

* [中文官方文档](https://www.tslang.cn/index.html)
* 这里就不教大家怎么安装typescript了, 大家可以去看下[官方安装教程](https://www.tslang.cn/docs/handbook/typescript-in-5-minutes.html) 里面有着详细安装介绍
* 安装完成后, 大家可以创建个学习typescript的demo



## 基础类型

* ##### boolean

  ```typescript
  let bl: Boolean = true
  
  console.log(bl)
  ```

* ##### number

  ```typescript
  let num: Number = 1
  let binaryLiteral: number = 0b1010;
  num = 2
  
  console.log(num)
  ```

  >  Tip: number 支持2, 8, 10, 16进制字面量

* ##### string

  ```typescript
  let str: String = '123' // ES5
  let Str: String = `String` // ES6
  
  console.log(str, Str)
  ```

* ##### array

  ```typescript
  let arr: Number[] = [num, 2, 3] // 写法1
  let arr2: Array<String> = [str, Str, '1'] // 写法2
  
  console.log(arr, arr2)
  ```

* ##### 元组Tuple

  > 元组类型允许表示一个已知元素数量和类型的数组(**即固定长度和类型的数组**)

  ```typescript
  let tuple: [String, Number, Boolean]
  tuple = ['1', 2, true]
  ```

* ##### 枚举 enum

  > `enum`类型是对JavaScript标准数据类型的一个补充。 像C#等其它语言一样，使用枚举类型可以为一组数值赋予友好的名字。

  * 数字类型枚举, 允许我们将数字类型或者其他任何与数字类型兼容的类型赋值给枚举类型的实例。

    ```typescript
    enum Color {
        red, // 0
        green, // 1
        blue // 2
    }
    // 编译为js
    var Color;
    (function (Color) {
        Color[Color["red"] = 0] = "red";
        Color[Color["green"] = 1] = "green";
        Color[Color["blue"] = 2] = "blue";
    })(Color || (Color = {}));
    // 结果
    Color = {
      0: "red",
      1: "green",
      2: "blue",
      blue: 2,
      green: 1,
      red: 0
    }
    ```

    > Tip: 默认情况下，第一个枚举值是 `0`，然后每个后续值依次递增 1
    >
    > ​	但是，你可以通过特定的赋值来改变给任何枚举成员关联的数字, 如下: 

    ```typescript
    enum Color {
      DarkRed = 3, // 3
      DarkGreen, // 4
      DarkBlue // 5
    }
    ```

  * 字符串枚举

    ```typescript
    enum EvidenceTypeEnum {
      UNKNOWN = '',
      PASSPORT_VISA = 'passport_visa',
      PASSPORT = 'passport'
    }
    // 结果
    EvidenceTypeEnum = {
      UNKNOWN: '',
      PASSPORT_VISA: 'passport_visa',
      PASSPORT: 'passport',
    }
    ```

  * 有静态方法枚举

    > 使用 `enum` + `namespace` 的声明的方式向枚举类型添加静态方法。

    ```typescript
    enum Weekday {
      Monday,
      Tuseday,
      Wednesday,
      Thursday,
      Friday,
      Saturday,
      Sunday
    }
    
    namespace Weekday {
      export function isBusinessDay(day: Weekday) {
        switch (day) {
          case Weekday.Saturday:
          case Weekday.Sunday:
            return false;
          default:
            return true;
        }
      }
    }
    
    const mon = Weekday.Monday;
    const sun = Weekday.Sunday;
    
    console.log(Weekday.isBusinessDay(mon)); // true
    console.log(Weekday.isBusinessDay(sun));
    ```

  * 开放式枚举

    > 通过之前ts枚举编译为js的代码中我们可以发现, 它会在匿名自执行函数中传入**同枚举名称相同的变量**,这意味着你可以**跨多个文件拆分（和扩展）枚举定义**

    ```typescript
    enum Color {
      Red, // 0
      Green, // 1
      Blue // 2
    }
    
    enum Color {
      DarkRed = 2, // 因枚举值为2, 会覆盖掉Blue
      DarkGreen,
      DarkBlue
    }
    // 结果
    Color = {
        0: "Red",
        1: "Green",
        2: "DarkRed",
        3: "DarkGreen",
        4: "DarkBlue",
        Blue: 2,
        DarkBlue: 4,
        DarkGreen: 3,
        DarkRed: 2,
        Green: 1,
        Red: 0
    }
    ```

* ##### any

  > 顾名思义, `any`代表该变量可以为任何类型, `typescript`跳过该变量类型检测

  ```typescript
  let number: any = 1
  let string: any = '1'
  ```

* ##### void

  > 函数无返回值其返回类型为`void`
  >
  > 声明一个void类型的变量没有什么大用，因为你只能为它赋予`undefined`和`null`

  ```typescript
  let fun = (): void => {
    console.log('fun')
  }
  let unusable: void = null    
  ```

* ##### undefined & null

  ```typescript
  let u: undefined = undefined;
  let n: null = null;
  ```

* ##### never

  > `never`类型表示的是那些永不存在的值的类型。

  ```typescript
  // 返回never的函数必须存在无法达到的终点
  function error(message: string): never {
      throw new Error(message);
  }
  
  // 推断的返回值类型为never
  function fail() {
      return error("Something failed");
  }
  
  // 返回never的函数必须存在无法达到的终点
  function infiniteLoop(): never {
      while (true) {
      }
  }
  ```

* ##### object

  ```typescript
  let obj: object = {}
  ```



## 总结

​	以上就是对typescript的基础类型进行的一些简单的总结, 可以看到ts在原生js已有的类型上, 加入了元组, 枚举.

​	在别的语言中, 枚举类型是强类型的，从而保证了系统安全性。枚举可以限定参数的个数，对调用者的行为能更加严格地进行控制。**把一些运行期的参数检查放到了编译期**，这点很重要。

​	同样元组也是**预先定义数组的长度以及类型**, 可以替开发者在赋值时进行检测.

​	 ts使js这门弱类型语言有了强类型的属性, 也体现了ts的一个核心原则: 对值所具有结构进行**类型检查**



## 参考

* [官方文档-基础类型](https://www.tslang.cn/docs/handbook/basic-types.html)

* [深入理解TypeScript](https://jkchao.github.io/typescript-book-chinese/typings/enums.html#%E6%95%B0%E5%AD%97%E7%B1%BB%E5%9E%8B%E6%9E%9A%E4%B8%BE%E4%B8%8E%E5%AD%97%E7%AC%A6%E4%B8%B2%E7%B1%BB%E5%9E%8B)