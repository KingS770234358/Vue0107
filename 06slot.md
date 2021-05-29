06slot ---- 承载分发内容的出口
<!DOCTYPE html>
<html lang="en" xmlns:v-bind="http://www.w3.org/1999/xhtml">
<head>
    <meta charset="UTF-8">
    <title>slot测试</title>
    <!--v-cloak 解决闪烁问题-->
    <style>
        [v-cloak] {
            display: none;
        }
    </style>
</head>
<body>
<div id="vue" v-cloak>
    <myslot>
    ###################################################################################################
        3.1把组件cominslot1-coursenames放入组件myslot中的名为slot1的插槽之中
        :coursenames 等价于 v-bind:coursenames="coursenamesindata"
        将组件中的props属性集合中的coursenames属性与vue实例中data里的数据coursenamesindata绑定
    ###################################################################################################
        <cominslot1-coursenames slot="slot1" :coursenames="coursenamesindata"></cominslot1-coursenames>
    ####################################################################################################    
        3.2v-for 创建多个 cominslot1-coursenames
        每个这个组件的slot都为slot2 把这些组件都会按序放入组件myslot中的名为slot2的插槽之中
        v-for="c in coursesindata" 遍历vue实例中的data中的数组coursesindata
        :coursename="c" 等价于 v-bind:coursename="c"
        将组件中的props属性集合中的coursename属性与vue实例中data里的数组coursesindata中当前遍历到的值绑定
    ####################################################################################################
        <cominslot2-coursename slot="slot2" v-for="c in coursesindata" :coursename="c"></cominslot2-coursename>
    </myslot>
</div>
<!--引入 JS 文件-->
<script src="../js/vue.js"></script>
<script src="../js/axios.js"></script>
<script type="text/javascript">
    // 2.1.定义要放入插槽slot1的组件
    Vue.component("cominslot1-coursenames",{
        props: ['coursenames'],
        template: '<div>{{coursenames}}</div>'
    })
    // 2.2.定义要放入插槽slot2的组件
    Vue.component("cominslot2-coursename",{
        props: ['coursename'],
        template: '<li>{{coursename}}</li>'
    })
    // 1.定义一个包含插槽组件 这个组件使用的标签除了插槽部分 其他都用自己的
    // 如 这里的 div 和 ur
    Vue.component("myslot",{
        template: '<div>' +
                        '<slot name="slot1"></slot>' +
                        '<ul>' +
                            '<slot name="slot2"></slot>' +
                        '</ul>' +
                    '</div>'
    })
    // ViewModel对象
    let vm = new Vue({
        el: '#vue',
        data: {
            msg: "hello world",
            coursenamesindata: "课程名称",
            coursesindata: ["java","c++","c"]
        },
    });
</script>

</body>
</html>

### 对比fragment
fragment:我们可以下一个页面A,然后把它定义成一个fragment片段,并给它取一个fragment名字,
         然后需要引入这个片段的页面B可以通过指定fragment名字的形式把A页面主动的引入进来
slot:在组件B中定义了一系列的插槽,这些插槽可以放入其他的多个组件
     使用了组件B之后,在组件B的标签内部使用组件A,A主动的在标签中指定slot属性来指定插槽名来表示自己想要放入组件B的哪个插槽之中
前者大页面B主动的引入小页面A
后者小组件A主动插入到大组件B的插槽之中