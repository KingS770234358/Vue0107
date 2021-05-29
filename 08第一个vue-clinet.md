08第一个vue-clinet

·安装环境:Nodejs
·测试环境:node -v
         npm -v
Nodejs相当于linux、anaconda、python
npm就是一个软件包管理工具,类似linux的apt,anaconda的conda,pip
·安装Nodejs淘宝镜像加速器(cnpm)
·在配置文件D:\NodeJS\node_modules\npm\npmrc中配置
 默认的包安装路径 [修改了包的安装路径的话 要把包的安装路径配置到环境变量里 这样npm下载的包的命令才能直接使用 比如vue]
 缓存路径
 镜像源
·全局安装vue-cli                                   npm install vue-cli -g
·查看可以基于哪些模板创建vue应用程序                 vue list
 类似maven可以创建普通的maven项目 也可以创建web的maven项目
 一般选择基于[webpack模板]创建,因为vuejs基于ES6,而大多数浏览器支持ES5
 因此需要使用webpack给vue项目进行打包降级[兼容]大多数浏览器

vue-cli
·vue-cli是vue官方提供的一个脚手架,用于快速生成一个vue的项目模板
·预先定义好的[目录结构]和[基础代码],类似创建Maven项目可以创建出一个骨架项目
·主要的功能:
 统一的目录结构
 本地调试
 热部署
 单元测试
 集成打包上线

创建第一个vue-cli程序
· 命令行进入要创建项目的目录里  [dos命令跨盘访问 cd /d D:\IDEA\workspace\vue_learning]
· 运行命令vue init webpack 08firstVue  [使用vue命令创建一个webpack类型的vue-cli项目 项目名为08firstVue]
  以下步骤里,括号里的都是默认值
  - 确认项目名==>项目名不能有大写...08firstvue
  - 输入项目的描述
  - 输入作者
  - vue build(可上下选择)                                  这里直接选第一项 运行时编译
  - 是否安装vue-router                                     这里选择不安装 体验手动实现
  - Use ESLint to lint your code                          这里选no
  - 是否安装测试                                           这里选no
  - Setup e2e tests with Nightwatch                       这里选no
  - 项目创建后是否自动运行npm install 命令(可上下选择)       这里选择no 体验手动实现
· 进入项目目录 08firstvue
  运行命令npm install 安装项目所需要的所有依赖环境
  若在add...下面一行出现found xx vulnerable等信息说明出错,[按照提示run .... to fix 命令行中运行命令....修复即可]
  安装是[根据项目目录里的package.json进行依赖的安装]
  安装完毕之后可以进入项目目录下的node_modules文件夹查看刚刚安装的依赖包
· 在项目文件夹里运行npm run dev命令 启动项目
  这一步自动使用webpack进行打包
  编译完成后 跳出地址供访问这个项目 [默认8080端口 可以设置]
  ------------这就是一个nodejs服务器 类似tomcat
  ctrl+c即可停止
· 使用IDEA直接open这个项目文件夹[目录结构]
  -在IDEA的命令行终端启动该项目
   直接使用npm run dev 可能报错:不是内部或外部命令,也不是可运行的程序
  [需要找到IDEA.exe 右键-属性-兼容性-以管理员身份运行此程序]
  - index.html是整个项目的主入口[在main.js中进行了绑定]
  -package.json相当于pom.xml文件
  -源码目录src
  1.main.js ====> 项目入口文件-所有组件最终的整合以及整个项目的配置
  import App from './App'  [//从./App.vue文件中引入名为App的组件]
  new Vue({                [=======创建Vue vm实例======]
    el: '#app',
    components: { App },   [//引入后将其放入vm实例中的组件数据才能使用]
    template: '<App/>'
  })
  2.App.vue ====>可以理解成整合了全部组件的应用组件
  第一部分: template标签里面定义了该组件的模板
  第二部分: script标签
           import HelloWorld from './components/HelloWorld' [引入组件文件夹下的其他组件]
           export default { [// 定义用于导出(被其他文件引用)对象]
             name: 'App',   [// 其他组件通过 name 即可引入该组件]
             components: {  [// 将该组件引入的其他组件包含进来]
               HelloWorld
             }
           }
  第三部分: style标签之间设置该组件的层叠样式
  3.component文件夹[用于存放自定义组件]
  HelloWorld为默认生成的自定义组件 结构同2
  - build目录(用于构建项目)
    'use strict' ES6使用严格检查模式
    webpack.base.conf.js
    module.exports
    entry 定义了项目的入口是main.js文件
    resolve和module定义了资源过滤 类似maven的build
  - config目录
    dev-env.js 配置当前的环境 [决定使用 webpack.base/dev/prod.conf.js]
    index.js   
       配置项目启动端口
       静态资源存放目录
  - node_modules目录 相当于java开发中的 lib dependencies