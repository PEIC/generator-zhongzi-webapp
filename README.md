###使用方法
grunt是运行在node上的命令行工具。

首先安装grunt

```zhongzi-webapp
npm install -g grunt-cli
```
除了grunt外我们还要用到yeoman，它主要用来搭建项目基础的结构，相当于给项目搭建一个基础的脚手架。
yeoman提供了许多不同项目的generator供安装，我们在这里直接使用我们编写并发布到npm上的zhongzi-webapp。
yeoman的安装命令为

```
npm install -g yo
```
然后我们把zhongzi-webapp构建器安装到本地。

```
npm install -g generator-zhongzi-webapp
```
建立项目文件夹并进入这个文件夹。

执行

```
yo zhongzi-webapp
```
来通过zhongzi-webapp构建器创建项目。
这时安装依赖的npm模块可能会花好长时间。安装完成后项目文件结构如下。

```

├── app
│   ├── common
│   │   ├── footer.html
│   │   └── header.html
│   ├── css
│   │   └── style.css
│   ├── images
│   │   ├── logo.png
│   │   └── test
│   │       └── logo.png
│   ├── index.html
│   ├── js
│   │   └── test.js
│   └── less
│       └── style.less
├── node-modules
├── Gruntfile.js
└── package.json
```
项目的新建到这里就结束了，grunt的相关配置也已经在项目中定义好了。下面就进入开发流程了。

主要实现的功能有：less编译、文件的复制、文件的删除、图片的优化、监听、页面分模块编译、静态服务器、打开浏览器。

把这些功能归类集成为3个方法。

####默认方法：

输入```grunt```执行。

下面的任务会自动执行，大概流程是先判断本地是否存在编译过的文件夹，没有的话自动执行build方法，有就跳过build阶段，接下来connect建立本地服务器，然后是open打开浏览器，最后执行watch监听文件变化，watch的功能是当监听的文件发生改动时执行定义的任务。less文件发生变化就编译样式到开发文件夹和编译后的文件夹，当html文件发生变化includes编译html，图片添加时自动拷贝到编译文件夹即预览文件夹。

####build方法
输入```grunt build```执行。

这时会执行build方法，build自动执行的大概流程是先clean删除之前编译好的文件夹，然后依次编译html，编译样式，拷贝静态资源。

####imagmin方法
输入```grunt imgmin```执行。
imgmin的流程是先删除编译文件夹里的images文件夹，然后优化开发文件夹images里的图片输出到编译文件夹中。

项目暂时还比较初级，构建工具也比较基础。工具会在投入生产后根据使用时遇到的问题再继续优化。
