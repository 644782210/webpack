### <div style="text-align: center;">webpack的安装与使用</div>
****
##### 首先介绍一下什么是webpack
Webpack 是一个模块打包器。它将根据模块的依赖关系进行静态分析，然后将这些模块按照指定的规则生成对应的静态资源。

_ _ _

##### Webpack 的特点
###### 1、代码拆分：
Webpack 有两种组织模块依赖的方式，同步和异步。异步依赖作为分割点，形成一个新的块。在优化了依赖树后，每一个异步区块都作为一个文件被打包。

###### 2、Loader：
Webpack 本身只能处理原生的 JavaScript 模块，但是 loader 转换器可以将各种类型的资源转换成 JavaScript 模块。这样，任何资源都可以成为 Webpack 可以处理的模块。

###### 3、智能解析：
Webpack 有一个智能解析器，几乎可以处理任何第三方库，无论它们的模块形式是 CommonJS、 AMD 还是普通的 JS 文件。甚至在加载依赖的时候，允许使用动态表达式 require("./templates/" + name + ".jade")。

###### 4、插件系统：
Webpack 还有一个功能丰富的插件系统。大多数内容功能都是基于这个插件系统运行的，还可以开发和使用开源的 Webpack 插件，来满足各式各样的需求。

###### 5、快速运行：
Webpack 使用异步 I/O 和多级缓存提高运行效率，这使得 Webpack 能够以令人难以置信的速度快速增量编译。

*****
##### 准备开始安装
---
    注意！！！
    在安装webpack之前，首先要安装 Node.js， Node.js 自带了软件包管理器 npm，Webpack 需要 Node.js v0.6 以上支持，建议使用最新版 Node.js。
---
用 npm 安装全局 Webpack：

---
	$ npm install webpack -g
---

此时 Webpack 已经安装到了全局环境下，可以通过命令行 webpack -h 试试。

通常我们会将 Webpack 安装到项目的依赖中，这样就可以使用项目本地版本的 Webpack。

---
    # 进入项目目录
    # 确定已经有 package.json，没有就通过 npm init 创建
    # 安装 webpack 依赖
    $ npm install webpack --save-dev
---

Webpack 目前有两个主版本，一个是在 master 主干的稳定版，一个是在 webpack-2 分支的测试版，测试版拥有一些实验性功能并且和稳定版不兼容，在正式项目中应该使用稳定版。

---
	# 查看 webpack 版本信息
	$ npm info webpack
    注意！！如果没有显示版本信息，则代表没有安装成功。
---
****

#####　webpack的使用
首先创建一个静态页面 index.html 和一个 JS 入口文件 entry.js：

HTML

---
    <!-- index.html -->
    <html>
    <head>
      <meta charset="utf-8">
    </head>
    <body>
      <script src="bundle.js"></script>
    </body>
    </html>
---


- - -
javascript
// entry.js 文件夹

---
    
	document.write('It works.')
---

- - -

然后编译 entry.js 并打包到 bundle.js：

---
	$ webpack entry.js bundle.js
---

打包过程会显示日志：

---
        Hash: e964f90ec65eb2c29bb9
    Version: webpack 1.12.2
    Time: 54ms
        Asset     Size  Chunks             Chunk Names
    bundle.js  1.42 kB       0  [emitted]  main
       [0] ./entry.js 27 bytes {0} [built]
---


- - -
用浏览器打开 index.html 将会看到 It works. 。

接下来添加一个模块 module.js 并修改入口 entry.js：

---
	// module.js
	module.exports = 'It works from module.js.'
---

---
    // entry.js
    document.write('It works.')
    document.write(require('./module.js')) // 添加模块
---

重新打包 webpack entry.js bundle.js 后刷新页面看到变化 It works.It works from module.js.