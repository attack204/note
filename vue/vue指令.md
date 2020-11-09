

<!-- TOC -->

- [插值表达式](#插值表达式)
- [vue指令](#vue指令)
  - [v-cloak延缓编译](#v-cloak延缓编译)
  - [v-text](#v-text)
  - [v-html显示html元素](#v-html显示html元素)
  - [v-pre显示原始信息](#v-pre显示原始信息)
  - [v-once关闭响应式](#v-once关闭响应式)
  - [v-model数据绑定](#v-model数据绑定)
  - [v-on事件绑定](#v-on事件绑定)
    - [事件绑定中的传参](#事件绑定中的传参)
  - [v-bind 可以动态的修改元素的属性值](#v-bind-可以动态的修改元素的属性值)
- [v-bind用于样式处理](#v-bind用于样式处理)
  - [用v-bind来动态处理class](#用v-bind来动态处理class)
  - [用v-bind来处理style样式](#用v-bind来处理style样式)
- [v-if等分支结构](#v-if等分支结构)
- [v-for循环](#v-for循环)
  - [带索引](#带索引)
  - [不带索引](#不带索引)
  - [访问对象](#访问对象)
  - [利用`:key`来提高访问速度](#利用key来提高访问速度)
  - [v-for与v-if同时使用](#v-for与v-if同时使用)
  - [注意：v-for的自动化渲染问题](#注意v-for的自动化渲染问题)
  - [注意：v-for索引的作用域](#注意v-for索引的作用域)
  - [注意：v-for="i in (1, 4)"自动生成区间问题](#注意v-fori-in-1-4自动生成区间问题)

<!-- /TOC -->




## 插值表达式

插值表达式可以简单理解为形如`{{x}}`的语句

x可以是表达式，简单的javascript语句

如果需要在自定义属性部分使用插值表达式的话可以使用`v-bind`

```html
<input type="text"  v-bind:value="Number(NumA) + Number(NumB)">
```


## vue指令

指令的格式: 以v开始

v-cloak, v-text, v-html都是数据绑定指令

 

### v-cloak延缓编译

1. 用途

解决插值表达式的闪动问题

当让所有实例加载完毕之后再显示

### v-text

1. 用途

填充纯文本

2. 实例

```html
<div v-text="123"></div> /*填充div内容为123*/
<div v-text="msg"></div> /*填充div内容为msg变量所指向的内容*/
```

3. 注意

其中的变量会被解析成对应的值



### v-html显示html元素

1. 用途

用于填充html元素

2. 实例

```html
<div v-html="msg"></div>
/*
若msg的内容为`<h1>HelloWorld</h1>`时，数据会被解析为一级标题HelloWorld
而若把v-html改为v-text，则数据会被解析为`<h1>HelloWorld</h1>`
*/
```


### v-pre显示原始信息

1. 用途

显示原始信息，跳过编译过程
 
比如不想让插值表达式的内容解析时，可以加此自定义属性

2. 实例

```html
 <div v-pre>{{msg}}</div>

 /*不会显示msg所绑定的数据，而会显示`{{msg}}`*/
```

### v-once关闭响应式

1. 用途

使标签内的元素不再具有响应式

保证里面的内容只编译一次

2. 实例

### v-model数据绑定

1. 用途

实现双向的数据绑定

多用于用户的输入域

关于双向绑定是指的：用户<->页面

当用户的输入发生改变时，页面内的数据也发生改变

当页面内的数据发生改变时，用户的输入也发生改变

2. 实例

注意，v-model与所作用的插值表达式不在同一个被管理的元素下时，v-model不会起任何作用

```html
<div id="app">
    <div>{{msg}}</div>
</div>
<input type="text" v-model="msg"/>
```

例如此代码，修改input标签中的内容时，{{msg}}的内容不会发生任何改变

但是若把input放到app里面，则可以实现数据的双向绑定

```html
<div id="app">
    <div>{{msg}}</div>
    <input type="text" v-model="msg"/>
</div>
```

3. 注意

`v-model`一般仅用于输入输出框，因为其目的是为了实现数据的绑定。

而在p标签中，则不能使用v-model，因为不能改变数据，如果想要展示内容，可以用v-text

4. v-model的底层实现

本质上还是用bind输出数据，然后把用户输入的数据覆盖掉原来的数据再输出

![](http://cdn.attack204.com/20201018213634.png)

### v-on事件绑定

1. 用途

用于绑定事件

2. 实例

* 每次点击按钮，可以实现当前页面中的num++

```html
<div id="app">
    <div>{{num}}</div>
    <input type="button" v-on:click="num++"/ value="Hello">
    <!--以下为简写模式 -->
    <!-- <input type="button" @click="num++"/ value="Hello"> -->
</div>
<script>
    vm = new Vue({
        el : "#app",
        data : {
            num : 0
        }

    })
</script>
```

* 用函数(方法)的写法

```html
<div id="app">
    <div>{{num}}</div>
    <input type="button" @click="handle"/ value="Hello">
    <input type="button" @click="handle()"/ value="Hello">
    <!--这两种写法都是一样的-->
</div>
<script>
    vm = new Vue({
        el : "#app",
        data : {
            num : 0
        },
        methods : {
            handle : function() {
                //这里必须加this，不然分不清是哪一个
                //这里的this就是指的当前的vue对象
                console.log(this);
                this.num++;
            }
        }

    })
</script>
```

#### 事件绑定中的传参

首先两种写法所传递的参数是不同的

```html
<input type="button" @click="handle"/ value="Hello">
<!--上面仅会传递默认的$event一个参数-->
<input type="button" @click="handle(123, 456, $event)"/ value="Hello">
<!--上面的会传递三个参数，但是注意，$event必须放在最后(好像不放在最后也行....)-->
```

实例

```html
<div id="app">
    <div>{{num}}</div>
    <input type="button" @click="handle"/ value="LGJGGGG">
    <input type="button" @click="handle(123,  $event,456)"/ value="ZGLnb">
</div>
<script>
    vm = new Vue({
        el : "#app",
        data : {
            num : 0
        },
        methods : {
            handle : function(p1, event, p2) {
                console.log(p1);
                console.log(event.target.tagName);
                console.log(p2);
            }
        }

    })
</script>
```

### v-bind 可以动态的修改元素的属性值

属性里面可以写一些data数据中的或者是插值运算符

注意在写插值运算符的时候不需要加`{{}}}`，在html标签中加的意义在于让html标签进行识别，而`v-bind`已经提醒浏览器转化识别方式了

update in 2020.10.22

事实上，v-bind会把双引号内的东西全部解析为变量，如果需要拼接的话，需要在其中加单引号，例如

```html
 <img class="Image2" v-if="(index)==flag" v-bind:src="'./img/'+index+'.jpg'">
```

**实际上v-指令内部相当于一段js代码**

这也是vue灵活度高的原因

## v-bind用于样式处理

### 用v-bind来动态处理class
   
用法1：用对象的方法设置每个class的状态

```html
<div v-bind:class="{class1 : state1, class2 : state2}"></div>

<script>
    var vm = new Vue({
        el:"#app",
        data: {
            state1 : 1,
            state2 : 0
        }, 
        methods : {
            change : function() {
                this.state1 = !this.state1;
                this.state2 = !this.state2;

            }
        }
    })
</script>

```


用法2：用数组的方法设置每个class的状态

与上面相差不是很大，感觉比上面的还垃圾。。。。。


```html
    <div id="app">
        <div v-bind:class="[C1, C2]"></div>
        <input type="button" value="click here and open new world" v-on:click="change">
    </div>

    <script>
        var vm = new Vue({
            el:"#app",
            data: {
                C1 : "class1",
                C2 : ""
            }, 
            methods : {
                change : function() {
                    this.C1 = "";
                    this.C2 = "class2";
                }
            }
        })
    </script>
```


注意事项： 

对象和数组可以结合使用，并且可以嵌套使用

### 用v-bind来处理style样式

没怎么学，感觉用处不大，看官网吧

[style样式处理](https://cn.vuejs.org/v2/guide/class-and-style.html#%E7%BB%91%E5%AE%9A%E5%86%85%E8%81%94%E6%A0%B7%E5%BC%8F)

## v-if等分支结构

就是根据data列表里面的值进行判断

注意v-if后面的flag

v-show：本质上是设置display:none;

v-if控制是否渲染，v-show控制是否显示

注意: v-if里面的判断条件是动态的，当其判断列表内的值发生改变时，会再进行判断

```html
<div id="app">
    <div v-if="flag==1" class="c1"> 1</div>
    <div v-else-if="flag==2" class="c2">2</div>
    <div v-else="flag==3" class="c3">3</div>
    <!-- 注意v-if后面的符号，是少见的= -->
    <el-button type="primary" v-on:click="ChangeColor" >ClickHere</el-button>
</div>
   
```


```html
<html>

<head>
    <meta charset="utf-8">
    <title>VueStudy</title>
    <script src="./js/vue.js"></script>
    <link rel="stylesheet" href="https://unpkg.com/element-ui/lib/theme-chalk/index.css">
    <script src="https://unpkg.com/element-ui/lib/index.js"></script>
    <style>
        * {
            transition: all 1s;
        }
        .c1 {
            width: 100px;
            height: 100px;
            background-color: #f00;
        }
        .c2 {
            width: 100px;
            height: 100px;
            background-color: #0f0;
        }
        .c3 {
            width: 100px;
            height: 100px;
            background-color: #00f;
        }
    </style>
</head>

<body>
    <div id="app">
        <div v-if="flag==1" class="c1"> 1</div>
        <div v-else-if="flag==2" class="c2">2</div>
        <div v-else="flag==3" class="c3">3</div>
        <!-- 注意v-if后面的符号，是少见的= -->
        <el-button type="primary" v-on:click="ChangeColor" >ClickHere</el-button>
    </div>
    <script>
        var vm = new Vue({
            el: "#app",
            data: {
                flag: 1,
            },
            methods: {
                ChangeColor : function() {
                    this.flag = (this.flag) % 3 + 1;
                }
            }
        })
    </script>


</body>

</html>
```

## v-for循环

首先得有数据，在data里定义一下即可，主要是有以下两种写法



### 带索引

```html
<div v-for="(item, index) in flag">{{item}}, {{index}}</div>
```

注意：`(item, index)`的位置不可更改。实际上是这样的，item和index都是我们自己起的名字，item对应的是第一个值，而vue规定第一个值就是对象本身

### 不带索引

```html
<div v-for="item in flag">{{item}}</div>
```

### 访问对象

如果数组内的元素是对象的话，需要用`.`来指定到底要访问什么

```html
<html>

<head>
    <meta charset="utf-8">
    <title>VueStudy</title>
    <script src="./js/vue.js"></script>
    <link rel="stylesheet" href="https://unpkg.com/element-ui/lib/theme-chalk/index.css">
    <script src="https://unpkg.com/element-ui/lib/index.js"></script>
    <style>
        * {
            transition: all 1s;
        }
        .c1 {
            width: 100px;
            height: 100px;
            background-color: #f00;
        }
        .c2 {
            width: 100px;
            height: 100px;
            background-color: #0f0;
        }
        .c3 {
            width: 100px;
            height: 100px;
            background-color: #00f;
        }
    </style>
</head>

<body>
    <div id="app">
        <el-button type="primary" v-on:click="ChangeColor" >ClickHere</el-button>
        <div v-if="if_show==1">
            <div v-for="item in flag">
                    {{item.first_key}}
                    {{item.second_key}}
            </div>
        </div>
    </div>
    <script>
        var vm = new Vue({
            el: "#app",
            data: {
                if_show : 0, 
                flag : [{first_key : "attack gg",
                        second_key : "attack cai"},
                        {first_key : "attack gg",
                        second_key : "attack cai"},
                        {first_key : "attack gg",
                        second_key : "attack cai"},
                       ],
            },
            methods: {
                ChangeColor : function() {
                    this.if_show = !this.if_show;
                }
            }
        })
    </script>


</body>

</html>
```

### 利用`:key`来提高访问速度

只需要让key匹配到后面的某个索引即可

例如`<div :key="item.id"> </div>`

```html
<html>

<head>
    <meta charset="utf-8">
    <title>VueStudy</title>
    <script src="./js/vue.js"></script>
    <link rel="stylesheet" href="https://unpkg.com/element-ui/lib/theme-chalk/index.css">
    <script src="https://unpkg.com/element-ui/lib/index.js"></script>
    <style>
        * {
            transition: all 1s;
        }
        .c1 {
            width: 100px;
            height: 100px;
            background-color: #f00;
        }
        .c2 {
            width: 100px;
            height: 100px;
            background-color: #0f0;
        }
        .c3 {
            width: 100px;
            height: 100px;
            background-color: #00f;
        }
    </style>
</head>

<body>
    <div id="app">
        <el-button type="primary" v-on:click="ChangeColor" >ClickHere</el-button>
        <div v-if="if_show==1">
            <div :key="item.id" v-for="item in flag">
                    {{item.first_key}}
                    {{item.second_key}}
            </div>
        </div>
    </div>
    <script>
        var vm = new Vue({
            el: "#app",
            data: {
                if_show : 0, 
                flag : [{
                            id : "1",
                            first_key : "attack gg",
                            second_key : "attack cai",
                        },
                        {
                            id : "2",
                            first_key : "attack gg",
                            second_key : "attack cai",
                        },
                        {
                            id : "3",
                            first_key : "attack gg",
                            second_key : "attack cai",
                        },
                       ],
            },
            methods: {
                ChangeColor : function() {
                    this.if_show = !this.if_show;
                }
            }
        })
    </script>


</body>

</html>
```

### v-for与v-if同时使用

### 注意：v-for的自动化渲染问题

考虑以下代码

```html
<div v-for="(item, index) in ImageData">
    <img class="Image2" v-if="(index + 1)==flag" v-bind:src="item.path"> 
</div>
```

按照正常的逻辑，当v-for执行完成之后，整个dom结构已经确定，此时再改变flag的值，dom结构也不会再发生改变。

但实际上，vue做的非常人性化，当其检测到ImageData中的元素发生改变时，会再次进行渲染。

### 注意：v-for索引的作用域

考虑以下代码(没错就是上面那段)

v-for生成的是相同的结构，但实际上在之后的代码中，仍然可以使用index, item这两个变量

即item和index这两个变量的作用域为自己和它所有的子标签

```html
<div v-for="(item, index) in ImageData">
    <img class="Image2" v-if="(index + 1)==flag" v-bind:src="item.path"> 
</div>
```

### 注意：v-for="i in (1, 4)"自动生成区间问题

有时候我们需要生成一段连续的数，vue提供了类似于python的generator。

考虑以下代码

```html
 <div class="NavigationItem" v-for="i in (1, 4)" v-on:click="SetFlag(i)">Image{{i}}</div>
```

其生成的dom结构如下(没错很神奇生成了四个)

```html
<div id="Navigation">
    <div class="NavigationItem">Image1</div>
    <div class="NavigationItem">Image2</div>
    <div class="NavigationItem">Image3</div>
    <div class="NavigationItem">Image4</div>
    <div class="ClearFlot"></div>
</div>
```










