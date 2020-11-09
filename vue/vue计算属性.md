# vue计算属性

本质上是提供了一种对字符串进行封装的方法

**计算属性与方法的最大不同在于计算属性有缓存机制**，在进行运算时效率更高一些。

计算属性的依赖是data中的数据，当data中的数据发生改变时，computed内的值也会发生改变




## 实例

例如反转字符串

需要注意reverse后面是不需要加()的

```html
<html>

<head>
    <meta charset="utf-8">
    <title>VueStudy</title>
    <script src="./js/vue.js"></script>
    <link rel="stylesheet" href="https://unpkg.com/element-ui/lib/theme-chalk/index.css">
    <script src="https://unpkg.com/element-ui/lib/index.js"></script>
    <script src="./js/vue.js"></script>
    <style>
        body {
            background-color: #eee;
        }
    </style>
</head>

<body>
    <div id="app">
        <div>
            {{msg}}
        </div>
        <div>
            {{reverse}}
        </div>
    </div>

    <script>
        vm = new Vue({
            el: "#app",
            data: {
                msg: "Hello",
            },
            computed: {
                reverse: function () {
                    return this.msg.split('').reverse().join('');
                }
            }
        })
    </script>



</body>

</html>
```





