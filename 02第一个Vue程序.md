# 02第一个Vue程序
vue框架图.png 
vue是MVVM模式的实现者

[viewModel]
· 能够观察到数据的变化,并对视图对应的内容进行更新
· 能够监听到视图的变化,并能够通知数据发生改变

优点:
· 特别小 易于上手 特别好用
· 吸收了Angular(MVVM)和React(虚拟DOM)的长处
· 自己的特色功能:计算属性 
· 开源、社区活跃度高

前端开发工具:
· Vsconde
· HBuilder
· Sublime Text
· WebStorm
· IDEA

MVVM
· MVVM模式和MVC模式一样,主要目的是分离视图(View)和模型(Model)
· 为什么要使用MVVM
  - 低耦合:视图View可以独立于Model变化和修改,一个ViewModel可以绑定到多个不同的view上
    当view变化的时候,model可以不变;当model变化的时候View也可以不变
  - 可复用: 可以把一些[视图逻辑]放在一个ViewModel里面,让多个View重复这段视图逻辑
  - 独立开发: 开发人员可以专注于业务逻辑和数据的开发(ViewModel),设计人员可以专注于页面设计
  - 可测试: 界面以前是比较难于测试的,现在可以针对ViewModel来写
  
第一个Vue程序=====[安装vue插件]
步骤:
1.IDEA创建空项目
2.新建module
3.创建html
· 引入vue包 <script src="../vue.js"></script>
<!-- view层 模板 -->
<div id="app">
    {{msg}}  <!-- DOM监听 数据绑定 -->
</div>
<script>
    // ViewModel对象=============>双向绑定层 完全解耦了View和Model
    var vm = new Vue({
        el: "#app",
        // Model
        data:{
            msg: "hello world"
        }
    });
</script>

·三个要素:View ViewModel Model
·数据Model存在与ViewModel对象之中
·在浏览器控制台进行测试:改变Model之中的值, 可以[不用刷新页面,动态的改变所绑定的View中的数据]
 它并没有去操作DOM,而DOM元素中的值发生了改变==================>虚拟DOM
 ViewModel : JavaScript Runtime Compiler 即时运行即时编译===>虚拟DOM
·对比以往的静态页面html,html中的数据是写死的,改变之后需要刷新网页才能看到改变效果
·el 和 data是七大属性其中两个
### IDEA 右键 new editFileTemplate Files + 可以给特定的文件新增模板