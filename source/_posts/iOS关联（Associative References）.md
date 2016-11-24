---
title: iOS关联（Associative References）
date: 2016-11-24 15:25:06
tags: 
	- iOS
	- Objective-C
	- 记录
	
---
### Objective-C Runtime(Associative References)

```objectivec 
// Sets an associated value for a given object using a given key and association policy.
OBJC_EXPORT void objc_setAssociatedObject(id object, const void *key, id value, objc_AssociationPolicy policy)
    OBJC_AVAILABLE(10.6, 3.1, 9.0, 1.0);

// Returns the value associated with a given object for a given key.
OBJC_EXPORT id objc_getAssociatedObject(id object, const void *key)
    OBJC_AVAILABLE(10.6, 3.1, 9.0, 1.0);

// Removes all associations for a given object.
// The main purpose of this function is to make it easy to return an object to a "pristine state”. You should not use this function for general removal of associations from objects, since it also removes associations that other clients may have added to the object. Typically you should use objc_setAssociatedObject(_:_:_:_:) with a nil value to clear an association.
OBJC_EXPORT void objc_removeAssociatedObjects(id object)
    OBJC_AVAILABLE(10.6, 3.1, 9.0, 1.0);
```
### 参数解释
object: 关联的源对象。
key: 相当于NSDictionary的键，不同的是关联对象是通过判断两个key的地址是否相等而不是具体的值来比较。
value: 关联的对象。
objc_AssociationPolicy: 与声明属性对应的内存管理方式。

| objc_AssociationPolicy			   | @property           |
| --------------------------------- |:-------------------:|
| OBJC_ASSOCIATION_ASSIGN           | (assign)            |
| OBJC_ASSOCIATION_RETAIN_NONATOMIC | (nonatomic, retain) |
| OBJC_ASSOCIATION_COPY_NONATOMIC   | (nonatomic, copy)   |
| OBJC_ASSOCIATION_RETAIN           | (retain)            |
| OBJC_ASSOCIATION_COPY             | (copy)              |

<!--more-->
### 使用
　　iOS关联，在不用继承的情况下将现有的两个对象关联起来。如果给现有的类存放一些额外信息，通常是继承一个类，然后定义新增加的属性，然而也可以通过关联给这个对象一个属性，而不用新加子类，在不用继承的情况下将现有的两个对象关联起来，可以对已有的类添加属性。

```objectivec 
static char key;
//关联的对象
NSString *value = @"我是关联的对象";
//关联的源对象
NSObject *obj = [[NSObject alloc] init];
    
objc_setAssociatedObject(obj, &key,value, OBJC_ASSOCIATION_RETAIN_NONATOMIC);
    
NSString *result = objc_getAssociatedObject(obj, &key);
    
NSLog(@"value = %@ result = %@", value, result);
``` 
　　关联还可以给对象增加属性，使Category不仅可以为现有类增加方法，还可以增加实例属性。

```objectivec 
#import <UIKit/UIKit.h>

@interface UILabel (Associate)

@property (nonatomic, strong) UIColor *placeholderColor;

@end
``` 

```objectivec
#import "UILabel+Associate.h"
#import <objc/runtime.h>

static char placeholderKey;

@implementation UILabel (Associate)

- (void)setPlaceholderColor:(UIColor *)placeholderColor
{
    objc_setAssociatedObject(self, &placeholderKey, placeholderColor, OBJC_ASSOCIATION_RETAIN_NONATOMIC);
}

- (UIColor *)placeholderColor
{
    return objc_getAssociatedObject(self, &placeholderKey);
}

@end
``` 
　　还可以关联一个block来简化代码。

```objectivec
static char alertViewKey;

- (void)showAlert {
	UIAlertView *alert = [[UIAlertView alloc]initWithTitle:@"提示" message:@"我是关联block" delegate:self cancelButtonTitle:@"取消" otherButtonTitles:@"确定", nil];
    
    void (^alertBlock)(NSInteger) = ^(NSInteger buttonIndex) {
        NSLog(@"我是关联block buttonIndex = %ld", (long)buttonIndex);
    };
    
    objc_setAssociatedObject(alert, &alertViewKey, alertBlock, OBJC_ASSOCIATION_COPY);//将block 与alert关联
    
    [alert show];
}

-(void)alertView:(UIAlertView *)alertView clickedButtonAtIndex:(NSInteger)buttonIndex
{   
    void(^ alertBlock)(NSInteger) = objc_getAssociatedObject(alertView, &alertViewKey);
    alertBlock(buttonIndex);
}
``` 
###　断开关联
　　使用`objc_removeAssociatedObjects`可以断开所有的关联，使用这个函数会断开所有的关联，把对象恢复到“原始状态”。