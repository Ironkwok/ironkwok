---
title: Xcode8遇到的一些事
date: 2016-10-18 10:10:10
tags: 
- Xcode
---
### 普通账号真机调试	
　　普通开发者账号有了限制，每七天可以创建10个APP IDs，可以使用同一个Bundle Identifier来规避这个问题。

### Xcode杂乱无章日志 
　　Xcode8里边 Edit Scheme-> Run -> Arguments, 在Environment Variables里边添加
OS_ACTIVITY_MODE，value值设置为disable...........添加后点击Close。
如果写了之后还是打印log，请重新勾选对勾，就可以解决了。
### 代码注释
　　这个是因为苹果解决xcode ghost，把插件屏蔽了。
　　解决方法是打开终端，命令运行：

``` bash
$ sudo /usr/libexec/xpccachectl
``` 
　　然后必须重启电脑后生效。

　　注意：Xcode8内置了开启注释的功能 Editor->Structure->Add Documentation。
<!--more--> 
### 关于CAAnimationDelegate
　　iOS9及以前: 

``` objectivec
/* Delegate methods for CAAnimation. */

@interface NSObject (CAAnimationDelegate)

/* Called when the animation begins its active duration. */

- (void)animationDidStart:(CAAnimation *)anim;

/* Called when the animation either completes its active duration or
 * is removed from the object it is attached to (i.e. the layer). 'flag'
 * is true if the animation reached the end of its active duration
 * without being removed. */

- (void)animationDidStop:(CAAnimation *)anim finished:(BOOL)flag;

@end
``` 
　　iOS10:

``` objectivec
/* Delegate methods for CAAnimation. */

@protocol CAAnimationDelegate <NSObject>
@optional

/* Called when the animation begins its active duration. */

- (void)animationDidStart:(CAAnimation *)anim;

/* Called when the animation either completes its active duration or
 * is removed from the object it is attached to (i.e. the layer). 'flag'
 * is true if the animation reached the end of its active duration
 * without being removed. */

- (void)animationDidStop:(CAAnimation *)anim finished:(BOOL)flag;

@end
``` 
　　变化就是iOS10之前CAAnimationDelegate只是基类的分类方法，是扩展，iOS10之后变成了协议，那么适配就应该分版本配置：

``` objectivec
#if __IPHONE_OS_VERSION_MAX_ALLOWED >= 100000

@interface ViewController () <CAAnimationDelegate>

#else

@interface ViewController ()

#endif
``` 