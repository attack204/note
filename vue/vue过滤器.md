# vue过滤器

过滤器是用来处理数据的，其可以对数据进行一些简单的操作。

其实通过其他方法也可以实现(watch等)，但是用filter会显得更简介，逻辑更清晰

## vue过滤器实现将字符串的前两个字符转化为大写

```html
<div id="app">
    <div>Please input username</div>
    <input type="text" name="" id="" v-model = "UserName">
    <div>The username that after transform is</div>
    <div>{{UserName | Upper}}</div>
</div>

<script>
    Vue.filter('Upper', function(val) {
        return String.fromCharCode(val.charCodeAt(0) - 32) + 
                String.fromCharCode(val.charCodeAt(1) - 32) + 
                val.slice(2, val.length);
        //切莫忘这个return;
    });
    var vm = new Vue({
        el: "#app",
        data: {
            UserName: "",
        },

    });
</script>
```

## 定义为局部过滤器

```html
<div id="app">
    <div>Please input username</div>
    <input type="text" name="" id="" v-model = "UserName">
    <div>The username that after transform is</div>
    <div>{{UserName | Upper}}</div>
</div>

<script>
    var vm = new Vue({
        el: "#app",
        data: {
            UserName: "",
        },
        //注意这里是filters, 不是filter
        filters: {
            Upper: function(val) {
                return String.fromCharCode(val.charCodeAt(0) - 32) + val.slice(1, val.length);
            },
        },

    });
</script>
```

## 过滤器传参

过滤器的后面可以用`()`来传递参数

```html
<div id="app">
    <div>Please input username</div>
    <input type="text" name="" id="" v-model = "UserName">
    <div>The username that after transform is</div>
    <div>{{UserName | Upper(1)}}</div>
    <div>{{UserName | Upper(2)}}</div>
    <!--也可以传递多个参数 Upper(1, 2, 3)-->
</div>

<script>
    var vm = new Vue({
        el: "#app",
        data: {
            UserName: "",
        },
        //注意这里是filters, 不是filter
        filters: {
            Upper: function(val, opt) {
                if(opt == 1) 
                    return String.fromCharCode(val.charCodeAt(0) - 32) + val.slice(1, val.length);
                else 
                    return val.charAt(0) + String.fromCharCode(val.charCodeAt(1) - 32) + val.slice(2);
            },
        },

    });
</script>

```







