# CSS 居中对齐
---

CSS 居中对齐相关的问题和总结。

### 水平居中

#### 水平居中行级元素或行盒(display 为 inline 或 inline-*)
```
.parent { text-align: center; }
```

#### 水平居中块级元素(display 为 block)
```
// 块级元素默认占满全部宽度，所以要设置 width
.element {
  margin: 0, auto;
  width: 100px;
}
```

#### 水平居中多个块级元素
块级元素默认堆叠排列，想要在一行上排列多个跨级元素，要将 display 设置为 inline-block.

```
.parent { text-align: center; }
.child {
  display: inline-block;
}
```

或者可以用flex布局：

```
.parent {
  display: flex;
  justify-content: center;
}
```

### 垂直居中
CSS 中有 vertical-align 这个属性，顾名思义就是垂直居中，那么是不是用这个属性就好。很遗憾不可以，这个属性指定行内元素与行基线的对齐方式，也就是说它的作用范围在一行上，并不适合在块级元素里面垂直居中对齐子元素。当然也有例外，下面会提到。

#### 垂直居中行级元素

##### 单行
可以设置上下相等的padding:

```
.element { padding: 20px 0; }
```

或者指定 line-height 等于 height：

```
.center-text {
  height: 100px;
  line-height: 100px;
}
```

##### 多行
多行的情况也可以设置上下的padding。

或者可以设置 display 为 table，对于 table-cell 而言 vertical-align 确实是垂直居中的，这就是前面提到的特列。

```
.parent {
  display: table;
}
.child {
  display: table-cell;
  vertical-align: middle;
}
```

当然flex布局也可以轻松的实现：

```
.parent {
  display: flex;
  flex-direction: column;
  justify-content: center;
  height: 200px;
}
```

另外还有一种使用CSS伪元素的实现方式：

```
.parent:before {
  content: ' ';
  display: inline-block;
  height： 100%；
  vertical-align: middle;
}

.child {
  display: inline-block;
  vertical-align: middle;
}
```

#### 垂直居中块级元素

##### 高度已知
```
.parent {
  postion: relative;
}
.child {
  position: absolute;
  top: 50%;
  height: 100px;
  margin-top: -50px;
}
```
##### 高度未知
```
.parent { position: relative; }
.child {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
}
```

或者使用flex布局。

### 绝对居中(同时水平和垂直居中) 
#### 高度宽度已知
```
.parent { position: relative; }
.child {
  width: 300px;
  height: 100px;
  padding: 20px;
  
  position: absolute;
  top: 50%;
  left: 50%;
  margin: -70px 0 0 - 170px;
}
```

#### 高度宽度未知
```
.parent { position : relative; }
.child {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
```

#### flex布局
```
.flex-parent {
  display: flex;
  justify-content: center;
  align-items: center;
}
```

### 总结

CSS 中有很多的方式可以实现居中对齐，包括水平居中和垂直居中，只是需要在不同情况下找到合适的方法。另外flex布局设计的更清晰，功能更强大，所以允许的话多考虑flex布局的方式。

***

参考：[Centering in CSS]
[Centering in CSS]:https://css-tricks.com/centering-css-complete-guide/#center-horizontally