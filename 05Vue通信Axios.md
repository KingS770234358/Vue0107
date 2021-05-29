05Vue通信Axios

本节课狂神博客:https://blog.kuangstudy.com/index.php/archives/595/

Axios Axios.js
官网: http://www.axios-js.com/
github: https://github.com/axios/axios
Axios的功能:
· 从浏览器中创建XMLHttpRequests
· 从Node.js中创建http请求
· 支持Promise API (JS中的链式编程)
· 拦截请求和响应
· 转换请求数据和响应数据
· 取消请求
· 自动转换JSON数据
· 客户端支持防御XSRF(跨站请求伪造)

Vue实例的生命周期 详见05VUE实例的声明周期.pdf
开始创建->初始化数据->编译模板->挂载DOM->渲染->更新->渲染、卸载等一系列过程

·使用axios获取本地data.json中的数据
 知识点:
 1.vue实例的生命周期 mounted()钩子函数的使用 data()函数的使用
 2.解决Vue的闪烁问题
<!DOCTYPE html>
<html lang="en" xmlns:v-bind="http://www.w3.org/1999/xhtml">
<head>
    <meta charset="UTF-8">
    <title>狂神说Java</title>
    <!--v-cloak 解决闪烁问题-->
    <style>
        [v-cloak] {
            display: none;
        }
    </style>
</head>
<body>
<!-- 0.这里是整个vue还没有启动的时候
     使用 属性选择器 [v-cloak] 通过display: none;暂时先不显示页面
     从而解决vue的闪烁问题 视频中存在一些问题 使用v-clock控制台会报错
     https://www.jb51.net/article/92949.htm
 -->
<div id="vue" v-cloak>
    <div>名称：{{info.name}}</div>
    <div>地址：{{info.address.country}}-{{info.address.city}}-{{info.address.street}}</div>
    <!-- 这里要使用v-bind指令才能使用Model中的值给<a>标签的href属性赋值 -->
    <div>链接：<a v-bind:href="info.url" target="_blank">{{info.url}}</a> </div>
</div>

<!--引入 JS 文件-->
<script src="../js/vue.js"></script>
<script src="../js/axios.js"></script>
<script type="text/javascript">
    var vm = new Vue({
        el: '#vue',
        // data: {} 是Vue实例的属性
        // data(){}  是Vue实例的方法 接收数据的时候 以函数的形式返回
        // 在这里面 这一步最先执行 1.把这些数据放到html里面el指定的地方,因此这步数据都为初始值(这里为null)
        data() {
            return {
                info: {
                    name: null,
                    address: {
                        country: null,
                        city: null,
                        street: null
                    },
                    url: null
                }
            }
        },
        ###########################################################################################################
        // 2.这里接上面执行, 使用axios获得本地数据data.json 更新页面中的数据
        mounted() { //钩子函数
            axios
                // 填写一个url 请求资源(这里请求本地资源)
                .get('data.json')
                // response即为请求得到的响应
                // => 是ES6规范,得到相应之后的回调函数执行一些操作 可以通过=>(console.log(response.data))输出得到的数据
                // 这里执行一个赋值操作 更新Model里的数据 this.info = response.data
                .then(response => (this.info = response.data));
        }
        ###########################################################################################################
    });
</script>

</body>
</html>