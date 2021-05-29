04Vue组件 === 自定义html标签 === 相当于html中的fragment 使用基本的html标签组装而成
<!-- view层 模板 -->
<div id="app">
    <mycomponentname v-for="item in templateList" v-bind:propname="item"></mycomponentname>
</div>
<script>
    // 定义一个Vue组件
    Vue.component("mycomponentname",{
        props: ['propname'],
        template: '<li>{{propname}}</li>'
    });
    // ViewModel对象
    let vm = new Vue({
        el: "#app",
        // Model
        data:{
            msg: "hello world",
            templateList: ["java上","c++","Python"]
        }
    });
</script>

· 大致流程:
  先在vm对象的model中定义一个数组templateList
  然后定义自己的组件mycomponentname,这个组件就是<li>{{propname}}</li>,其中ff由props['propname']定义,将propname放入属性数组中
  ### 注意 mycomponentname  propname ### 
     不能使用全大写字母;不能使用驼峰命名;
     可以大写字母开头和全小写。。。
  然后使用自定义的组件 v-for 遍历数组templateList
  此时,item in templateList将数组中的每一个item 与属性propname 进行绑定 v-bind:propname="item",
  这样item传给propname,propname传到props里,最终才能传到<li>{{propname}}</li> 被template所引用