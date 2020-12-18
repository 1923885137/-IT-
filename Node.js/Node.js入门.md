#   执行node.js文件

>  可以使用cmd和powershell来执行js文件，但要注意执行的文件工作目录

##  如下图执行一个桌面的sever.js文件

![image-20201214224748885](D:\互联网专业知识\Node.js\imgs\image-20201214224748885.png)

> **还可以按住shift键，在工作目录下打开shell，这样就可以省去找到文件当前目录的步骤**

![](D:\互联网专业知识\Node.js\imgs\QQ截图20201214225509.png)

>  tab键还可以自动帮我们补全路径，按上键可以重复刚才执行的文件
>
> clear命令可以清屏

![](D:\互联网专业知识\Node.js\imgs\QQ截图20201214230153.png)

##  Node.js模块化开发

###   js开发的弊端

1.文件依赖

2.命名冲突

![](D:\互联网专业知识\Node.js\imgs\QQ截图20201214230411.png)

###   Node.js模块化开发规范

>  **node规定一个js文件就是一个模块，模块内部定义的变量和函数默认情况下在外部无法得到**

1.模块内部使用**export**s对象进行成员导出，使用**require**方法导入其他模块

![](D:\互联网专业知识\Node.js\imgs\QQ截图20201214231124.png)

#### 模块成员的导出

```javascript
//a.js
let version = 1.0
const sayHi = name =>`你好，${name}`;
//向模块外导出数据
exports.version = version;
expoerts.version = sayHi;
```

#### 模块成员导入

```javascript
//b.js
let a = require('./b.js');
//注意相对路径中./表示当前路径，在html中可以省略不写，但是在node.js中不行
//输出b模块中version变量
console.log(a.version);
console.log(a.sayHi('yes'));
```

>  模块导入的文件后缀是可以省略

#### 模块导出的另外一种方式

```javascript
const greeting = name => `hello ${name}`;
module.exports.greeting = greeting;
```

>  exports是module.exports的别名（地址引用关系），导出对象最终以module.exports为准

```javascript
module.exports.greeting = greeting;
module.exports = {
    name: 'zhangsan'
}
exports ={
    age: 'jjj'
}
//在b.js中
let a = require('./a.js');
console.log(a);
//输出 {
//    name: 'zhangsan'
//}
//当exports对象和module.exports对象指向的不是同一个对象时 以module.exports为准
```

### 系统模块

**我们称Node运行坏境提供的API为系统模块**

![](D:\互联网专业知识\Node.js\imgs\QQ截图20201215111025.png)

#### 文件操作

```javascript
//通过模块的名字fs对模块进行引用
const fs = require('fs');
//通过模块内部的readFile读取文件内容
fs.readFile('文件路径/文件名称'[,'文件编码'], callback);

//具体语法
//读取上一级css目录下的base.css
//读取文件中的相对路径是相对于，命令行的当前目录，更常用绝对路径更加安全，但require方法不需要忧虑
fs.readFile('../base.css','utf-8',(err,doc)=>{
    //如果读取文件错误， 参数err的值为错误对象，否则err的值为null
    //doc为文件内容
    if(err == null){
        console.log(doc);
    }
})

//写入文件内容（这个会覆盖掉原文件内容），没有这个文件时，系统会自动生成
fs.writeFile('文件路径/文件名称', '数据', callback);
const content = '<h3>正在使用fs.writeFile写入文件内容</h3>';
 fs.writeFile('../index.html', content, err => {
   if (err != null) { //err为null时，表示写入成功。
       console.log(err);
       return;
   }
   console.log('文件写入成功');
 });

```

#### 模块path路径操作

> 不同操作系统的路径分隔符不统一
>
> Windows 上是 \  /
>
> Linux 上是 /
>
> 路径拼接，path在内部实现的时候会判断当前的操作系统，然后使用相应系统的路径分隔符

```javascript
//路径拼接的语法
path.join('路径', '路径', ...)
          
 // 导入path模块
 const path = require('path');
  // 路径拼接
 let finialPath = path.join('itcast', 'a', 'b', 'c.css');
  // 输出结果 itcast\a\b\c.css
 console.log(finialPat);

//大多数情况下使用绝对路径，因为相对路径有时候相对的是命令行工具的当前工作目录
//在读取文件或者设置文件路径时都会选择绝对路径
//使用__dirname获取当前文件所在的绝对路径（有两个—）

//安全写法
const fs = require('fs');
const path = require('path');

console.log(__dirname);
console.log(path.join(__dirname, '01.helloworld.js'))

fs.readFile(path.join(__dirname, '01.helloworld.js'), 'utf8', (err, doc) => {
	console.log(err)
	console.log(doc)
});

```

### 第三方模块

​        **别人写好的、具有特定功能的、我们能直接使用的模块即第三方模块，由于第三方模块通常都是由多个文件组成并且被放置在一个文件夹中，所以又名包**

#### 第三方模块的两种形式

1. 以js文件的形式存在，提供实现项目具体功能的api接口
2. 以命令行工具形式存在，辅助项目开发

#### 获取第三方模块

npmjs.com：第三方模块的存储和分发仓库

npm (node package manager) ： node的第三方模块管理工具

![](D:\互联网专业知识\Node.js\imgs\QQ截图20201215200901.png)

**第三方模块nodemon**

nodemon是一个命令行工具，用以辅助项目开发。

在Node.js中，每次修改文件都要在命令行工具中重新执行该文件，非常繁琐。

![](D:\互联网专业知识\Node.js\imgs\QQ截图20201215201656.png)

遇到不能运行脚本的解决方法

![](D:\互联网专业知识\Node.js\imgs\QQ截图20201215202409.png)

> 如果想终止脚本的运行，可以按ctrl+c终止

**第三方模块 nrm**

![](D:\互联网专业知识\Node.js\imgs\QQ截图20201215202719.png)

## Gulp

```javascript
//项目上线，HTML、CSS、JS文件压缩合并
//语法转换（es6、less ...）
//公共文件抽离
//修改文件浏览器自动刷新
```

### Gulp的使用

```javascript
//使用npm install gulp下载gulp库文件
//在项目根目录下建立gulpfile.js文件
//重构项目的文件夹结构 src目录放置源代码文件 dist目录放置构建后文件
//在gulpfile.js文件中编写任务.
//在命令行工具中执行gulp任务
```

### Gulp中提供的方法

```javascript
//gulp.src()：获取任务要处理的文件
//gulp.dest()：输出文件
//gulp.task()：建立gulp任务
//gulp.watch()：监控文件的变化
const gulp = require('gulp');
  // 使用gulp.task()方法建立任务
 gulp.task('first', () => {
    // 获取要处理的文件
     //第一个参数，任务的名称，第二个参数，回调函数
    gulp.src('./src/css/base.css') 
    // 将处理后的文件输出到dist目录
    .pipe(gulp.dest('./dist/css'));
 });

```

>  面对如下错误的时候

![](D:\互联网专业知识\Node.js\imgs\QQ截图20201216100905.png)

可以参考https://www.gulpjs.com.cn/docs/getting-started/async-completion/

```javascript
const gulp = require('gulp');
gulp.task('first',(cb) =>{
    console.log('我们人生的第一个gulp');
     gulp.src('./src/base.css')
     .pipe(gulp.dest('dist/css'));
     cb();
});
```

### Gulp插件（一般在npm官网查用法）

```javascript
//gulp-htmlmin ：html文件压缩
//gulp-csso ：压缩css
//gulp-babel ：JavaScript语法转化
//gulp-less: less语法转化
//gulp-uglify ：压缩混淆JavaScript
//gulp-file-include 公共文件包含
//browsersync 浏览器实时同步

//html任务
//1.html文件中代码的压缩操作
//2.抽取html文件中的公共代码，然后插入到不同文件中对应位置写@@include('路径')；这里没有展示
const gulp = require('gulp');
const htmlmin = require('gulp-htmlmin');
gulp.task('htmlmin',(cb) =>{
   gulp.src('./src/*.html')
   .pipe(htmlmin({ collapseWhitespace: true }))
   .pipe(gulp.dest('dist'));
   cb();
});
//压缩css，和将less语法的转换
// 1.less语法转换
// 2.css代码压缩
const less = require('gulp-less');
const csso = require('gulp-csso');
gulp.task('cssmin', () => {
	// 选择css目录下的所有less文件以及css文件
	gulp.src(['./src/css/*.less', './src/css/*.css'])
		// 将less语法转换为css语法
		.pipe(less())
		// 将css代码进行压缩
		.pipe(csso())
		// 将处理的结果进行输出
		.pipe(gulp.dest('dist/css'))
});
// js任务
// 1.es6代码转换
// 2.代码压缩
const babel = require('gulp-babel');
const uglify = require('gulp-uglify');
gulp.task('jsmin', () => {
	gulp.src('./src/js/*.js')
		.pipe(babel({
			// 它可以判断当前代码的运行环境 将代码转换为当前运行环境所支持的代码
            presets: ['@babel/env']
        }))
        .pipe(uglify())
        .pipe(gulp.dest('dist/js'))
});
// 复制文件夹
gulp.task('copy', () => {

	gulp.src('./src/images/*')
		.pipe(gulp.dest('dist/images'));

	gulp.src('./src/lib/*')
		.pipe(gulp.dest('dist/lib'))
});
// 构建任务
gulp.task('default', ['htmlmin', 'cssmin', 'jsmin', 'copy']);//gulp会依次执行数组中的任务 
```

### package.json*文件*

```javascript
{
  "name": "gulp-demo",
  "version": "1.0.0",
  "description": "",
  "main": "gulpfile.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },//这里可以执行快捷命令
   //如我把"script"{
   //    "test": "echo \"Error: no test specified\" && exit 1",
   //    "build":"nodemon app.js"   
//}
//那么我们在命令行工具中输入npm run build就等价于nodemon app.js
  "author": "",
  "license": "ISC",
  "dependencies": {
    "mine": "^0.1.0"
  }
}
```



#### **1** node_modules*文件夹的问题

1.文件夹以及文件过多过碎，当我们将项目整体拷贝给别人的时候,，传输速度会很慢很慢. 

2.复杂的模块依赖关系需要被记录，确保模块的版本和当前保持一致，否则会导致当前项目运行报错

#### 2.**package.json****文件的作用**

项目描述文件，记录了当前项目信息，例如项目名称、版本、作者、github地址、当前项目依赖了哪些第三方模块等。

使用**npm init** **-y**命令生成。

>  若我们在接受别人项目的时候，别人没传node_modules，但有package.json

> 那么我们就可以在命令行工具中 使用npm install 就可以下载项目所需所有插件

![](D:\互联网专业知识\Node.js\imgs\QQ截图20201216222738.png)

>  只下载项目依赖文件 npm install  --production

> ![](D:\互联网专业知识\Node.js\imgs\QQ截图20201216223241.png)

>   

#### 3.**package-lock.json****文件的作用**

> 锁定包的版本，确保再次下载时不会因为包版本不同而产生问题

> 加快下载速度，因为该文件中已经记录了项目所依赖第三方包的树状结构和包的下载地址，重新安装时只需下载即可，不需要做额外的工作

### node.js中模块的加载机制

#### 模块查找规则-当模块拥有路径但没有后缀时

```javascript
require('./find.js');
require('./find');
//require方法根据模块路径查找模块，如果是完整路径，直接引入模块。
//如果模块后缀省略，先找同名JS文件再找同名JS文件夹
//如果找到了同名文件夹，找文件夹中的index.js
//如果文件夹中没有index.js就会去当前文件夹中的package.json文件中查找main选项中的入口文件
//如果找指定的入口文件不存在或者没有指定入口文件就会报错，模块没有被找到

```

#### ***模块查找规则当模块没有路径且没有后缀时**

```javascript
require('find');
//Node.js会假设它是系统模块
//Node.js会去node_modules文件夹中
//首先看是否有该名字的JS文件
//再看是否有该名字的文件夹,有的话执行q其中的index.js
//如果是文件夹看里面是否有index.js
//如果没有index.js查看该文件夹中的package.json中的main选项确定模块入口文件
//否则找不到报错

```

