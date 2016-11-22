---
title: 谈一谈NS_ENUM & NS_OPTIONS
date: 22016-11-11 16:33:08
tags: 
		- Objective-C 
		- iOS 
		- 探究
---
### 说明
　　enum枚举类型为预设值定义常量，没有被赋值的会自动从0开始赋予连续的值。有几种常用的枚举类型定义方式，每种方法大致相同，却也有细微的区别，现在就来探究一下究竟有何不一样。

``` objectivec
enum {
    MyEnumValueA,
    MyEnumValueB,
    MyEnumValueC,
};

typedef enum {
    MyEnumValueA,
    MyEnumValueB,
    MyEnumValueC,
} MyEnum;

typedef enum {
    MyEnumValueA,
    MyEnumValueB,
    MyEnumValueC,
};
typedef NSInteger MyEnum;
``` 
　　以上是之前的枚举类型，要么是定义了整型值，没有定义类型名，要么是没有定义类型名和enum什么关系，现在，枚举类型宏定义统一使用以下写法： 
> enumdef - Enumerated Type Declaration 

<!--more-->

``` objectivec
typedef enum : NSUInteger {
    MyEnumValueA,
    MyEnumValueB,
    MyEnumValueC,
} MyEnum;
``` 
> nsenum - Enumerated Type Declaration (NS_ENUM)
 
``` objectivec
typedef NS_ENUM(NSUInteger, MyEnum) {
    MyEnumValueA = 0,
    MyEnumValueB,
    MyEnumValueC,
}; 
``` 
　　这两种写法大致相同，都有两个参数，一个为值的类型，一个为枚举类型的名字，大括号里是要定义的枚举值，这种实现方法结合了之前版本的优点，写作也更加美观。
　　需要一提的是，还有另外一种枚举定义，NS_OPTIONS，使用位运算来赋值，其好处就是枚举值同时使用时仍具有唯一性，可使用或运算相加，位移不同位数得到的枚举值在二进制中代表不同的数位，不同的数位或运算的结果是唯一的。
> nsoptions - Enumerated Type Declaration (NS_OPTIONS) 

``` objectivec
typedef NS_OPTIONS(NSUInteger, MyEnum) {
    MyEnumValueA = 1 << 0,
    MyEnumValueB = 1 << 1,
    MyEnumValueC = 1 << 2,
}; 
``` 
　　可以在多条件下使用NS_OPTIONS，在结果唯一互斥的情况下使用NS_ENUM。