## 实例

vue实例大概长这样

vue的每层都是一种嵌套类的结构，以`:`分割

一个很奇怪的结论是: vue实例之内很少有`=`

```js
var vm = new Vue({
    el : "#VueApp",
    data : {
        NumA : "",
        NumB : "",
        Ans  : ""
    },
    methods : {
        Calc : function() {
            this.Ans = Number(this.NumA) + Number(this.NumB);
            console.log(this.Ans);
        }
    }
})
```