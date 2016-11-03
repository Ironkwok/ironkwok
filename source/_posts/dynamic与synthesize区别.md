---
title: dynamic与synthesize区别
date: 2016-07-24 19:15:14
tags: 
	- iOS 
	- Objective-C
	- Xcode
---

## @dynamic与@synthesize的区别
@property有两个对应的词，一个是@synthesize，一个是@dynamic，如果@synthesize和@dynamic都没有默认@synthesize。
@synthesize的语义是如果没有手动实现setter/getter方法，那么编辑器会自动为你加上这两个方法。
@dynamic是告诉编辑器，代码中用@dynamic修饰的属性，其setter/getter方法会在程序运行的时候或者其他方式动态绑定，以便让编译器通过编译，不自动生成setter/getter方法（对于readonly的属性只需提供getter方法即可）。假如一个属性被声明为@dynamic var，没有提供setter/getter方法，编译的时候没问题，但是当程序运行到instance.var = someVar，由于缺setter方法导致程序崩溃，或者当运行到someVar = var时，由于缺getter方法同样导致崩溃。编译时没问题，运行时才执行相应的方法，这就是所谓的动态绑定。
