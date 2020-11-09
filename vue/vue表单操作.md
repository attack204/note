# vue表单操作

## 禁止表单自动提交

考虑以下html

```html
<div id="app">
    <form action="http://www.baidu.com">
        <input type="submit" value="submit">   
    </form>
</div>
```

当点击submit的时候会自动提交表单，但是有时候我们并不想那么做，可以使用`@click.prevent=submit`来手写提交函数

## vue控制radio按钮

不太能理解原理，但改变gender的值的确可以选择第一个框或者第二个框。

update：理解了，官网上是这么说的

> v-model 会忽略所有表单元素的 value、checked、selected attribute 的初始值而总是将 Vue 实例的数据作为数据来源。你应该通过 JavaScript 在组件的 data 选项中声明初始值。



```html
<div id="app">
    <form action="http://www.baidu.com">
        <input type="radio" name="uname1" id="" value = "1" v-model="gender">
        <input type="radio" name="uname2" id="" value = "2" v-model="gender">
        <input type="submit" value="submit" @click.prevent="ban">   
    </form>
</div>

<script>
    var vm = new Vue({
        el: "#app",
        data: {
            flag: 1,
            gender: 2,
        },
        methods : {
            ban : function() {
                console.log("GG");
            }
        }
    })
</script>
```

## 表单修饰符

### .number将字符串转化为数字

`v-model.number="age"`可以将字符串转化为数字

### .trim去掉开始和结尾的修饰符

### .lazy将input事件转化为change事件(即失去焦点时才执行)

注意console语句与是否有.lazy有关













