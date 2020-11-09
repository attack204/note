# vue自定义指令

## vue自定义指令方法

```html
<script>
    Vue.directive('focus', {
        inserted : function(el) {
            el.focus();
        }
    })
    var vm = new Vue({
        el: "#app",
    })
</script>
```

## vue自定义指令获取元素属性

可以使用binding.value来获取=后面的内容

```html
<div id="app">
        <input type="text" id="" v-test="attack">
</div>
<script>
    Vue.directive('test', {
        inserted : function(el, binding) {//这句叫钩子函数
            //使用钩子函数中的binding
            el.focus();
            console.log(binding.value.attack2);
        }
    })
    var vm = new Vue({
        el: "#app",
        data : {
            attack : {
                attack2 : "123",
            },
        },
    })
</script>
```

## 局部指令

就是定义方式改了一下，改到了组件的内部，同时原来的`directive`变成了`directives`

```html
<div id="app">
    <input type="text" id="" v-color="InputColor">
</div>

<script>
    Vue.directive('color', {
        inserted : function(el, binding) {
            el.style.backgroundColor = binding.value;
        }
    });
    var vm = new Vue({
        el: "#app",
        data : {
            InputColor : "#0f0",
        },
        directives : {
            color : {
                inserted : function(el, binding) {
                    el.style.backgroundColor = binding.value;
                },
            },
        },
    })
</script>
```

## 实例

### 根据自定义属性改变元素的样式

```html
<div id="app">
    <input type="text" id="" v-color="InputColor">
</div>

<script>
    Vue.directive('color', {
        inserted : function(el, binding) {
            el.style.backgroundColor = binding.value;
        }
    });
    var vm = new Vue({
        el: "#app",
        data : {
            InputColor : "#0f0",
        },
    })
</script>
```


