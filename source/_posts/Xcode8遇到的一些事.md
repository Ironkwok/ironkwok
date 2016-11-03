---
title: Xcode8遇到的一些事
---
# Xcode8遇到的一些事
### 普通账号真机调试	
普通开发者账号有了限制，每七天可以创建10个APP IDs，可以使用同一个Bundle Identifier来规避这个问题。
### Xcode无脑日志 
Xcode8里边 Edit Scheme-> Run -> Arguments, 在Environment Variables里边添加
OS_ACTIVITY_MODE，value值设置为disable...........添加后点击Close。
如果写了之后还是打印log，请重新勾选对勾，就可以解决了。
### 代码注释
这个是因为苹果解决xcode ghost，把插件屏蔽了。
解决方法
打开终端，命令运行：
> $ sudo /usr/libexec/xpccachectl

然后必须重启电脑后生效。

注意：Xcode8内置了开启注释的功能 Editor->Structure->Add Documentation。
