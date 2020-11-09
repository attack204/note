# vue侦听器

vue侦听器用于数据变化时和开销较大的计算，和computed有类似的地方

## watch监听变量的变化

注意，watch后定义的内容中，对象的名称必须是data中的内容，因为这样才能监听到数据。

watch、computed、methods有时是可以互换的，比如下面这个例子。

但是有时候是不能用watch代替computed的


```html
    <div id="app">
        <input type="text" name="" id="" v-model.number="sum1">
        <input type="text" name="" id="" v-model.number="sum2">
        <div>{{sum1 + sum2}}</div>
        <div>{{handle()}}</div>
        <div>{{handle2}}</div>
        <div>{{sum3}}</div>
    </div>

    <script>
        var vm = new Vue({
            el: "#app",
            data: {
                sum1: 233,
                sum2: 12,
                sum3: "",
            },
            methods: {
                handle: function() {
                    return this.sum1 + this.sum2;
                }
            },
            computed: {
                handle2: function() {
                    return this.sum1 + this.sum2;
                }
            },
            watch: {
                sum1: function(val) {
                    this.sum3 = this.sum1 + this.sum2;
                },
                sum2: function(val) {
                    this.sum3 = this.sum1 + this.sum2;
                }
            }
        })

    </script>
```

## watch使用场景：验证用户名是否合法

```html
<div id="app">
    <div>请输入用户名</div>
    <input type="text" v-model.lazy="UserName" name="" id=""></input>
    <div>{{HINT}}</div>
</div>

<script>
    var vm = new Vue({
        el: "#app",
        data: {
            UserName: "",
            HINT: "",
        },
        watch: {
            UserName: function(val) {
                this.HINT = "正在检查是否合法";
                var that = this;
                //注意that的用法，setTimeout的this是windows，因此需要提前存一下that
                    
                //注意延时函数的用法
                setTimeout(function() {
                    if(val.length <= 6)
                        that.HINT = "不合法";
                    else 
                        that.HINT = "合法";
                }, 500)
                
            }
        },
    })
</script>

```