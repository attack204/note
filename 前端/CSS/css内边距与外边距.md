# css内边距与外边距

## 内边距与外边距的理解

### 理解方式

实际上任何一个块级元素都可以这样被理解

![](http://cdn.attack204.com/20200912195814.png)

重点是把content与border分开考虑

### 边距合并

某一元素的下边距为15px，某一元素的上边距为15px，则总共为15px;

### padding

padding在设立的时候内部元素的大小并不会改变，这是w3c制定的标准

理解上可能会存在误区

padding实际上和border差不多，并不会把元素往里面挤，而会往外面扩
