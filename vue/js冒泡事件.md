# js冒泡事件

## 冒泡机制复现

说白了就是某个元素被点击的时候，其父元素也会触发同样的事件

比如下列代码

当点击按钮的时候会弹出两个框，分别为`SonSon`和`FatherFather`


```html
<html>

<head>
    <meta charset="utf-8">
    <title>VueStudy</title>
    <script src="./js/vue.js"></script>
    <script src='./js/jquery.min.js'></script>
    <style>
        #FatherFather {
            width: 100px;
            height: 100px;
            background-color: #f00;
            margin-left: 300px;
        }
        #SonSon {
            margin-left: -300px;
        }
    </style>
</head>

<body>
    <div id="FatherFather">
        <div id="Father">
            <div id="Son">
                <button id="SonSon">123</button>
            </div>
        </div>
    </div>

</body>


<script>
    $("#SonSon").click(function () {
        alert($(this).attr("id"));
    })
    $("#FatherFather").click(function () {
        alert($(this).attr("id"));
    })

</script>

</html>
```

## 阻止冒泡事件


第一种写法，用原生的event属性来进行操作

```html
<html>

<head>
    <meta charset="utf-8">
    <title>VueStudy</title>
    <script src="./js/vue.js"></script>
    <script src='./js/jquery.min.js'></script>
    <style>
        #FatherFather {
            width: 100px;
            height: 100px;
            background-color: #f00;
            margin-left: 300px;
        }
        #SonSon {
            margin-left: -300px;
        }
    </style>
</head>

<body>
    <div id="My">
        <div id="FatherFather" v-on:click="handle2()">
            <div id="Father">
                <div id="Son">
                    <button id="SonSon" v-on:click="handle($event)">123</button>
                </div>
            </div>
        </div>
    </div>
</body>


<script>
    var vm = new Vue({
        el: "#My",
        methods: {
            handle: function (event) {
                alert(1);
                event.stopPropagation();
                
            },
            handle2: function () {
                alert("2");
            }
        }

    });

</script>

</html>
```

第二种写法，直接用
`v-on:click.stop`

```html
<html>

<head>
    <meta charset="utf-8">
    <title>VueStudy</title>
    <script src="./js/vue.js"></script>
    <script src='./js/jquery.min.js'></script>
    <style>
        #FatherFather {
            width: 100px;
            height: 100px;
            background-color: #f00;
            margin-left: 300px;
        }
        #SonSon {
            margin-left: -300px;
        }
    </style>
</head>

<body>
    <div id="My">
        <div id="FatherFather" v-on:click="handle2()">
            <div id="Father">
                <div id="Son">
                    <button id="SonSon" v-on:click.stop="handle()">123</button>
                </div>
            </div>
        </div>
    </div>
</body>


<script>
    var vm = new Vue({
        el: "#My",
        methods: {
            handle: function () {
                alert("1");
            },
            handle2: function () {
                alert("2");
            }
        }

    });

</script>

</html>
```


## 参考资料

[冒泡事件](https://blog.csdn.net/luanlouis/article/details/23927347)
