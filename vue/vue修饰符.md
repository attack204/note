# 修饰符

## 事件修饰符

首先要明白简单的事件。

比如最简单的冒泡事件(下面的参考资料中有对应的文章，说白了就是当一个按钮被点击时，他的所有父元素都会被点击)

```html
<button id="SonSon" v-on:click.stop="handle()">123</button>
```

加上`.stop`即可阻止冒泡

## 按键修饰符

可以指定按下某个键之后执行某个操作

比如最常见的一个业务场景，用户按下enter之后自动提交表单，可以用如下语句来实现

```html
<input type="button" value="submit" v-on:keyup.enter="submit">
```

```html
<html>

<head>
    <meta charset="utf-8">
    <title>VueStudy</title>
    <script src="./js/vue.js"></script>
    <style>

    </style>
</head>

<body>
    <div id="VueApp">
        用户名: <input type="text" v-model="UserName">
        <div></div>
        密码: <input type="text" v-model="UserPassword">
        <div></div>
        <input type="button" value="submit" v-on:keyup.enter="submit">
    </div>


    <script>
        var vm = new Vue({
            el: "#VueApp",
            data: {
                UserName: "",
                UserPassword: "",
            },
            methods: {
                submit: function () {
                    // alert(1);
                    console.log(this.UserName, this.UserPassword);
                }
            }

        })
    </script>


</body>

</html>
```



再比如用户需要删除某一行的内容，可以用`v-on:keyup.delete="ClearContent"`来实现

```html
用户名: <input type="text" v-model="UserName">
<input value="清除用户名" type="button" v-on:click="ClearUserName">
<div></div>
密码: <input type="text" v-on:keyup.delete="ClearUserPassword" v-model="UserPassword">
<input value="清除密码" type="button" v-on:click="ClearUserPassword">
<div></div>
<input type="button" value="submit" v-on:click="submit" v-on:keyup.enter="submit">
```


```html
<html>

<head>
    <meta charset="utf-8">
    <title>VueStudy</title>
    <script src="./js/vue.js"></script>
    <style>

    </style>
</head>

<body>
    <div id="VueApp">
        用户名: <input type="text" v-model="UserName">
        <input value="清除用户名" type="button" v-on:click="ClearUserName">
        <div></div>
        密码: <input type="text" v-on:keyup.delete="ClearUserPassword" v-model="UserPassword">
        <input value="清除密码" type="button" v-on:click="ClearUserPassword">
        <div></div>
        <input type="button" value="submit" v-on:click="submit" v-on:keyup.enter="submit">
    </div>


    <script>
        var vm = new Vue({
            el: "#VueApp",
            data: {
                UserName: "",
                UserPassword: "",
            },
            methods: {
                submit: function () {
                    console.log(this.UserName, this.UserPassword);
                },
                ClearUserName: function () {
                    this.UserName = "";
                },
                ClearUserPassword: function () {
                    this.UserPassword = "";
                }
            }

        })
    </script>


</body>

</html>
```


## 自定义按键运算符

首先需要获取到按键的代码，可以用event.keyCode来获取

```html
<html>

<head>
    <meta charset="utf-8">
    <title>VueStudy</title>
    <script src="./js/vue.js"></script>
    <style>

    </style>
</head>

<body>
    <div id="VueApp">
        <input type="text" v-on:keyup="GetCode">
    </div>


    <script>
        var vm = new Vue({
            el: "#VueApp",
            data: {

            },
            methods: {
                GetCode : function() {
                    console.log(event.keyCode);
                }
            }

        })
    </script>


</body>

</html>
```


接下来只需要在`keyup.`之后加上按键对应的数字即可

例如获取到上是38

则可以写`v-on:keyup.38="MoveTop"`

```html
<html>

<head>
    <meta charset="utf-8">
    <title>VueStudy</title>
    <script src="./js/vue.js"></script>
    <style>

    </style>
</head>

<body>
    <div id="VueApp">
        <input type="text" v-on:keyup.38="GetCode">
    </div>


    <script>
        var vm = new Vue({
            el: "#VueApp",
            data: {

            },
            methods: {
                GetCode : function() {
                    console.log(event.keyCode);
                }
            }

        })
    </script>


</body>

</html>
```

但是这样非常不直观

官网上提供了`Vue.config.keycodes.a = "38"`来进行重命名

这个a是可以自己改的，但是不能含有大写字母


```html
<html>

<head>
    <meta charset="utf-8">
    <title>VueStudy</title>
    <script src="./js/vue.js"></script>
    <style>

    </style>
</head>

<body>
    <div id="VueApp">
        <input type="text" v-on:keyup.MoveTop="GetCode">
    </div>


    <script>
        Vue.config.keyCodes.MoveTop = 38;
        var vm = new Vue({
            el: "#VueApp",
            data: {

            },
            methods: {
                GetCode : function() {
                    console.log(event.keyCode);
                }
            }

        })
    </script>


</body>

</html>
```


