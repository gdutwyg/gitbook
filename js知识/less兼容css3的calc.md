# less兼容css3的calc

### css3之calc
CSS3新出了一个calc计算属性，用于动态计算长度值，任何长度值都可以使用calc()函数进行计算；
calc()函数支持 "+", "-", "*", "/" 运算；

有关calc的文档可以看[这里](http://www.w3cplus.com/css3/how-to-use-css3-calc-function.html)

**例子**
```css
.main {
  padding-left: calc(50% - 50px); // .main宽度的50%再减去50px
}
```

### 问题
但是在less里面使用calc就会出现问题了
```css
.class {
  height: calc(100% - 50px); // less自己就把它当表达式计算掉了，导致到浏览器那里渲染成了calc(50%)
}
```

### 解决方法
**解决方法也挺简单，加上~用""包起来。**
```css
.class {
  height: calc(~"100% - 50px");
}
```

可如果要用变量怎么用呢？也不复杂，像下面这样就搞定啦
```css
.class {
  @cap: 50px;
  height: calc(~"100% - @{cap}");
}
```

