---
title: typeScript学习笔记
auth: charmingYouYou
categories: 
- typescript
tags: 
- typeScript
- 类型检测
---

# TypeScript学习笔记

> typeScript是js的超集, 具有类型检测功能

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

  * 参考来源: [深入理解TypeScript](https://jkchao.github.io/typescript-book-chinese/typings/enums.html#%E6%95%B0%E5%AD%97%E7%B1%BB%E5%9E%8B%E6%9E%9A%E4%B8%BE%E4%B8%8E%E5%AD%97%E7%AC%A6%E4%B8%B2%E7%B1%BB%E5%9E%8B)

