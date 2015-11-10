# 如何编写nodejs命令行模块？

上面给出的很多都是nodejs写的小工具模块，nodejs和npm的种种好处，使得nodejs开发命令行模块异常简单


先说一下node module的作用

- 封装常见类库
- 命令行工具

nodejs这几年之所以如此快的崛起，就是因为模块编写简单，npm无比强大

npm是nodejs最好的东西，常用分类

- 1）命令行工具
  - 比如express-generator
  - 比如gulp 和grunt
- 2）shell相关
  - 比如kp：根据端口杀死进程
  - 比如mongo-here：启动mongodb的简化写法
- 3）本地服务器
  - 比如je
  - 比如hade

用起来非常方便，虽然有在线的，但网络是一个障碍
尤其没网的时候就不能用，非常郁闷

具体做法

无论如何，它都值得你一学的

下面看一下如何编写nodejs命令行模块

## 创建git repo

github上创建即可

## git clone到本地

	git clone git@github.com:i5ting/node-cli-demo.git
	
##  切换到项目目录

	cd node-cli-demo

## 初始化npm

使用npm命令，初始化npm的配置文件package.json


执行

```
npm init
```

一直回车，除非你真的有东西想改动，具体如下

```
➜  node-cli-demo git:(master) npm init
This utility will walk you through creating a package.json file.
It only covers the most common items, and tries to guess sane defaults.

See `npm help json` for definitive documentation on these fields
and exactly what they do.

Use `npm install <pkg> --save` afterwards to install a package and
save it as a dependency in the package.json file.

Press ^C at any time to quit.
name: (node-cli-demo) 
version: (1.0.0) 
description: 
entry point: (index.js) 
test command: 
git repository: (https://github.com/i5ting/node-cli-demo.git) 
keywords: 
author: 
license: (ISC) 
About to write to /Users/sang/workspace/github/node-cli-demo/package.json:

{
  "name": "node-cli-demo",
  "version": "1.0.0",
  "description": "node-cli-demo =============",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "repository": {
    "type": "git",
    "url": "https://github.com/i5ting/node-cli-demo.git"
  },
  "author": "",
  "license": "ISC",
  "bugs": {
    "url": "https://github.com/i5ting/node-cli-demo/issues"
  },
  "homepage": "https://github.com/i5ting/node-cli-demo"
}


Is this ok? (yes) 
➜  node-cli-demo git:(master) ✗ 
```

## 创建文件

	mkdir bin
	mkdir test

	touch bin/node-cli-demo.js
	touch test/node-cli-demo.js

	touch index.js
	touch gulpfile.js


bin是可执行文件

test是放测试文件的目录

lib是模块的核心代码目录，一般是index.js找lib/xxx.js



 #!/usr/bin/env node

 console.log('hello node module')
 
 
## 修改package.json

### 命令配置（至关重要）

```
  "preferGlobal": "true",
  "bin": {
    "badge": "bin/badge.js"
  },
```

此处是关键

`preferGlobal`确定你的这个命令是不是全局的，一定要设置为true，不然不放到path里，不能全局用的。


`bin`是配置你的cli名称和具体哪个文件来执行这个的
	
### scripts

```
  "scripts": {
    "start": "npm publish .",
    "test": " node bin/badge.js -t js -n q "
  },
```

这里定义了2个命令

- `npm start`

这里我用它发布当前npm到npmjs.org上

- `npm test`

这里我用它作为测试代码，避免每次都重复输入

## 发布

发布之前要注册npmjs账户的

  npm login(只需要一次，以后就不用了)
	npm start


当然更多的时候，我们看到的命令是这样

➜  vsc-doc git:(master) ✗ cp --help
cp: illegal option -- -
usage: cp [-R [-H | -L | -P]] [-fi | -n] [-apvX] source_file target_file
       cp [-R [-H | -L | -P]] [
## 更多

推荐几个解析命令行args的库

- commander是tj写的，一个不错的库，目前用的最多的库
- yargs也不错，更强大，简洁，官方推荐
- ccli是我写的，封装了yargs和基本常用的库	

还有私有模块