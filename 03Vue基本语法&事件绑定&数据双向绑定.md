03Vue基本语法
1. 使用v-bind来绑定特定的元素
· 使用v-bind之后编译器提示自动导入命名空间
<span v-bind:title="msg">
    鼠标悬停几秒中查看此处动态绑定的提示信息!
</span>
title是span标签原有的属性:当鼠标悬停在span上的时候会显示title指定的值;
使用v-bind对title进行绑定,可以把ViewModel对象的Model中的数据msg动态的绑定到这个title属性上
### vue中 v-xxx等被称为[指令]
v-表示它们是Vue提供的特殊性, 它们会在渲染的DOM上应用特殊的响应式行为
[特殊指令 v-bind:tagAttrName="data" 绑定vm model里的数据data和标签的属性tagAttrName]

2.流程控制
  判断 v-if v-else-if v-else
  循环 v-for
### 当直接更改文件里的Model的时候 而不是在浏览器的控制台里进行值的修改 需要刷新页面才行
[7大属性: el data methods]

3.事件绑定(具体有哪些事件网上一大堆)
[特殊指令 v-on:eventName="respFunName" 将标签的eventName事件与vm对象methods里定义的函数respFunName绑定]

4.数据的双向绑定
·说明:之前在vm对象中定义data 使用{{}}方式取值,实现的是单向绑定
当在控制台改变vm对象中定义的data的值的时候,绑定处的视图显示的数据也会变化
·这里使用[v-model指令]实现数据的双向绑定:
 -当在控制台改变vm对象中定义的data的值的时候,绑定处的视图显示的数据也会变化
 -当在视图上改变值,比如在一个input text里面输入值的时候,使得vm对象中定义的data的值跟着改变
 -这个绑定是将标签的value属性和model中的数据绑定在一起 
  1)在单选框中 隐式自带checked属性 checked=(radio的value==vm的data的某个变量sex)
    当sex==value时,value对应的那个radio就会被选中,用于设置单选框的默认值
    当radio组里一个radio的check发生改变的时候,必有一个radio的checked属性为true,使得sex=checked为true的那个radio的value
  2)在复选框中 vm对象中要使用一个数组类型的变量和复选框双向绑定,用字符串类型绑定会出错
    可以在数组里存放现有的checkbox的value来进行默认选项的勾选
  3)下拉框
    要先加一个预留项 ----请选择----
    绑定方式与单选框相同
  ====> 使用v-model进行数据的双向绑定,与标签的value checked(单选框、复选框) selected(下拉框)属性息息相关
