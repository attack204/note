


# ES6

## let关键字

与var一样用来定义变量，不同的是，let所定义的变量是与代码块绑定的

比较常见的应用场景是for循环，即

```js
for(let i = 0; i < 10; i++) {
  
}
```

## const关键字

必须要赋初始值

const也具有块级作用域

## 解构赋值

可以简化定义变量时变量赋值操作

```js
<script>
  let [a, b, c] = [233, 114, 514];
  console.log(a);
  console.log(b);
  console.log(c);
  /*
  输出 233
        114
        514
  */
</script>
```

### 数组解构

以及从数组中提取元素操作

```js
<script>
  let arr = [1, 2, 3];
  let[a, b, c] = arr;
  console.log(a);
  console.log(b);
  console.log(c);
  /*
  输出1 2 3
  */
</script>
```

### 对象解构

直接看代码吧

- 注意：对象解构需要保证左侧的变量名与对象内的变量名相同

```js
<script>
  var at = {name: 'at',
            age:  '18'};
var {name, agee} = at;
//这个列表里必须是name, age
//如果按这个写成agee，那么agee为undefined
console.log(name);
console.log(age);
</script>
```

如果不想用对象内的变量名可以这么写

```js
<script>
  var at = {
    name: 'at',
    age : '18',
  };
  var {name: atname, age: atage} = at;
  console.log(atname);
  console.log(atage);
</script>

```


## 箭头函数

一种新的定义函数的方式

```js
//下面的三种写法是等价的
<script>
  function add(x, y) {
    return x + y;
  }
  const add1 = (x, y) => {
    return x + y;
  }
  const add2 = (x, y) => x + y;
  console.log(add(1, 2));
  console.logadd1(1, 2));
  console.log(add2(1, 2));
</script>
```

如果形参只有一个，形参外侧的小括号也可以省略掉


```js
<script>
  const f = v => alert(v);
  f(233);
</script>
```

### 箭头函数的this指针

箭头函数与普通函数的最大区别就在于，

箭头函数的this指针指向的是定义区域

大概是这样子的，由于obj对象不能算是定义区域，因此obj对象里的箭头函数相当于指向了windows

```js
var age1 = 20;
var obj = {
  age: 20,
  say: function() {
    console.log(this.age);
  },
  say1: () => {
    console.log(this.age);
    console.log(this.age1);
  }
}
obj.say();//20
obj.say1();//undefined 20
```


## 剩余参数

...args来表示剩余的元素，类型为数组(相当于一个不定长数组),
arga的名称可以自己指定

```js
<script>
  const sum = (a1, ...args) => {
    let s = a1;;
    for(let i = 0; i < args.length; i++)
      s += args[i];
    return s;
  }
  console.log(sum(1));
  console.log(sum(1, 2, 3, 4, 5));
</script>
```

### 剩余参数与解构赋值一起使用

```js
<script>
  let [s1, ...s2] = [1, 2, 3, 4, 5];
  console.log(s1);1
  console.log(s2);[2, 3, 4, 5]
</script>
```

### 剩余参数的扩展运算符

用途可以把伪数组(htmlCollection)转化为真正的数组

```js
<script>
  let a = document.getElementsByTagName("div");
  console.log(a);
  let b = [...a];
  console.log(b);
</script>
```

## from对象扩展

## find查找数组中符合条件的对象

## find查找数组中符合条件的对象的位置








