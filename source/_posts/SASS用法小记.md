---
title: SASS用法小记
date: 2016-06-18 16:46:53
type: "SASS"
tags: [SASS,CSS]
categories: [前端]
---

之前项目用LESS，现在新项目打算用SASS，所以做个主要常用知识点小记。

#### [在线编译地址](http://www.sassmeister.com/)


#### @import 引入
```
　@import "../binjs.scss";  // 引入文件
　@import "../huangyb.css"; 
```


#### @mixin 混入


>注意：LESS的变量用`@` , SASS是 `$` 

 - 带参数

```
@mixin borderSet($dott: solid, $color: #fcf) {
  border: 8px $dott $color;
}
div {
    opacity: 0;
    @include borderSet(dotted, #fa0); //带参数传入
}
```

- 不带参数 显示默认值 不定义参数值 就显示默认值

```
@mixin borderSet($dott: solid, $color: #fcf) {
  border: 8px $dott $color;
}
div {
    opacity: 0;
    @include borderSet; //不带参数传入 可括号 可不括号
}

```

#### 嵌套

> LESS也是一样的嵌套规则， `&` 符号都相同

- 使用&引用父元素
```
div {
    opacity: 0;
    @include borderSet(); //不带参数传入 可括号 可不括号
    &:after  {
      color:#ccc;
    } 
}
```

- 属性的嵌套
```
 p {
  border: {
    color:red;
    width:12px;
  }
}
```


#### 变量用 `#{}` 包裹

如果变量需要镶嵌在字符串之中，就必须需要写在#{}之中。一般来说，我们设置的变量都是用于属性值的，而如果用在属性或者选择器上，就得以#{}包裹起来了。

```
$className:huangyb;
.#{$className} {
  width: 12px;
}

// 解析成
.huangyb {
  width: 12px;
}
```
```
$side : left;
.#{$side} {
　　border-#{$side}-radius: 5px;
}
// 解析成
.left {
  　　border-left-radius: 5px;
}
```

#### !default 的使用

正常情况下 声明两个变量 会出现后面覆盖前面的变量
```
$color:red;
$color:blue;
p{
    color:$color; //blue
}
```

若声明了 `!default` 会就不能出现覆盖的现象

```
$color:red;
$color:blue !default;
p{
    color:$color; //red
}
```

#### 多个变量的声明

```
$linkColor: red blue;

a{
    color:nth($linkColor,1);
    &:hover{
        color:nth($linkColor,2);
    }
}

// 解析后
a {
  color: red;
}
a:hover {
  color: blue;
}

```

#### @extend 继承

```
div { 
  color:#fcf; 
  
}
p { 
  @extend div; 
  width:10px; 
}
span {
  @extend p;
}

// 解析后
div, p, span {
  color: #fcf;
}

p, span {
  width: 10px;
}

```



#### function 

```
@function binjs($value) {
  @return #{$value}px;
}

div {
  width: binjs(30);
}

//解析后
div {
  width: 30px;
}
```

####  @if @else 条件判断

```
$width:12px;
div {
  @if ($width>10) {
     color:#fcf;
  } @else {
    color:#fa0;;
  }
}
```


