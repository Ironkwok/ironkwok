---
title: Cannot find module DTraceProviderBindings

date: 2016-11-11 16:42:49

tags: 
	- hexo
	
---
### 针对这个错误网上解决办法贴的很多，却都没有解决我的问题，最终使用此办法：

``` bash
$ sudo npm uninstall -g hexo-cli
$ sudo npm install -g hexo-cli
``` 
### 解决办法如下：
　　网上无数答案，最靠谱的办法：

``` bash
$ npm install hexo --no-optional
``` 
　　然而，执行了之后没有效果，再找：

``` bash
$ npm uninstall hexo
$ npm install hexo --no-optional
``` 
　　并没有什么用，坚持不放弃，重装hexo-cli：

``` bash
$ npm uninstall -g hexo-cli
$ npm install -g hexo-cli
``` 
<!--more--> 
　　卸载时出现以下结果：

``` bash
npm ERR! Darwin 16.1.0
npm ERR! argv "/usr/local/bin/node" "/usr/local/bin/npm" "uninstall" "-g" "hexo-cli"
npm ERR! node v7.0.0
npm ERR! npm  v3.10.8
npm ERR! path /usr/local/lib/node_modules/hexo-cli/node_modules/ansi-regex
npm ERR! code EACCES
npm ERR! errno -13
npm ERR! syscall access

npm ERR! Error: EACCES: permission denied, access '/usr/local/lib/node_modules/hexo-cli/node_modules/ansi-regex'
npm ERR!  { Error: EACCES: permission denied, access '/usr/local/lib/node_modules/hexo-cli/node_modules/ansi-regex'
npm ERR!   errno: -13,
npm ERR!   code: 'EACCES',
npm ERR!   syscall: 'access',
npm ERR!   path: '/usr/local/lib/node_modules/hexo-cli/node_modules/ansi-regex' }
npm ERR! 
npm ERR! Please try running this command again as root/Administrator.
``` 
　　使用sudo，输入password，完美执行：

``` bash
$ sudo npm uninstall -g hexo-cli
$ sudo npm install -g hexo-cli
``` 
　　一试之下，顿觉开朗，不再报错，完美解决问题：

``` bash
$ hexo --version
hexo: 3.2.2
hexo-cli: 1.0.2
os: Darwin 16.1.0 darwin x64
http_parser: 2.7.0
node: 7.0.0
v8: 5.4.500.36
uv: 1.9.1
zlib: 1.2.8
ares: 1.10.1-DEV
icu: 57.1
modules: 51
openssl: 1.0.2j
``` 
### 错误说明：

``` bash
$ hexo --version
{ Error: Cannot find module './build/Release/DTraceProviderBindings'
    at Function.Module._resolveFilename (module.js:472:15)
    at Function.Module._load (module.js:420:25)
    at Module.require (module.js:500:17)
    at require (internal/module.js:20:19)
    at Object.<anonymous> (/usr/local/lib/node_modules/hexo-cli/node_modules/dtrace-provider/dtrace-provider.js:17:23)
    at Module._compile (module.js:573:32)
    at Object.Module._extensions..js (module.js:582:10)
    at Module.load (module.js:490:32)
    at tryModuleLoad (module.js:449:12)
    at Function.Module._load (module.js:441:3)
    at Module.require (module.js:500:17)
    at require (internal/module.js:20:19)
    at Object.<anonymous> (/usr/local/lib/node_modules/hexo-cli/node_modules/bunyan/lib/bunyan.js:79:18)
    at Module._compile (module.js:573:32)
    at Object.Module._extensions..js (module.js:582:10)
    at Module.load (module.js:490:32) code: 'MODULE_NOT_FOUND' }
{ Error: Cannot find module './build/default/DTraceProviderBindings'
    at Function.Module._resolveFilename (module.js:472:15)
    at Function.Module._load (module.js:420:25)
    at Module.require (module.js:500:17)
    at require (internal/module.js:20:19)
    at Object.<anonymous> (/usr/local/lib/node_modules/hexo-cli/node_modules/dtrace-provider/dtrace-provider.js:17:23)
    at Module._compile (module.js:573:32)
    at Object.Module._extensions..js (module.js:582:10)
    at Module.load (module.js:490:32)
    at tryModuleLoad (module.js:449:12)
    at Function.Module._load (module.js:441:3)
    at Module.require (module.js:500:17)
    at require (internal/module.js:20:19)
    at Object.<anonymous> (/usr/local/lib/node_modules/hexo-cli/node_modules/bunyan/lib/bunyan.js:79:18)
    at Module._compile (module.js:573:32)
    at Object.Module._extensions..js (module.js:582:10)
    at Module.load (module.js:490:32) code: 'MODULE_NOT_FOUND' }
{ Error: Cannot find module './build/Debug/DTraceProviderBindings'
    at Function.Module._resolveFilename (module.js:472:15)
    at Function.Module._load (module.js:420:25)
    at Module.require (module.js:500:17)
    at require (internal/module.js:20:19)
    at Object.<anonymous> (/usr/local/lib/node_modules/hexo-cli/node_modules/dtrace-provider/dtrace-provider.js:17:23)
    at Module._compile (module.js:573:32)
    at Object.Module._extensions..js (module.js:582:10)
    at Module.load (module.js:490:32)
    at tryModuleLoad (module.js:449:12)
    at Function.Module._load (module.js:441:3)
    at Module.require (module.js:500:17)
    at require (internal/module.js:20:19)
    at Object.<anonymous> (/usr/local/lib/node_modules/hexo-cli/node_modules/bunyan/lib/bunyan.js:79:18)
    at Module._compile (module.js:573:32)
    at Object.Module._extensions..js (module.js:582:10)
    at Module.load (module.js:490:32) code: 'MODULE_NOT_FOUND' }
hexo: 3.2.2
hexo-cli: 1.0.2
os: Darwin 16.1.0 darwin x64
http_parser: 2.7.0
node: 7.0.0
v8: 5.4.500.36
uv: 1.9.1
zlib: 1.2.8
ares: 1.10.1-DEV
icu: 57.1
modules: 51
openssl: 1.0.2j
``` 