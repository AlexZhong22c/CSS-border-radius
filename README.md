# 第三代圆角介绍：

（另，第一、第二代圆角见于上方demo）

先给出一个div作为演示用：

```html
<style>
    .basic {
      /*基本样式：*/
      width: 200px;
      height: 200px;
      border: 1px solid black;
    }
</style>
<div id="test" class="basic">test</div>
```

圆角边框border-radius可以为边框设置圆角(IE8-不支持)。

按照左上、右上、右下、左下的顺序可以设置四个角：

```html
#test {
border-radius: 23px 55px 31px 15px;
}
```

## 值的省略

1.如果省略左下值，左下角就和右上角样式相同：

```
#test {
border-radius: 23px 55px 31px;
}
```

2.如果再省略右下值，右下角就和左上角样式相同：

```
#test {
border-radius: 23px 55px;
}
```

3.如果再省略到剩下一个值，那就四个角样式一样。

## 值的拆分

```
#test {
border-radius: 23px 55px 31px 15px;
}
```

等价于 **圆角单角** 的写法：

```
#test {
border-top-left-radius: 23px;
border-top-right-radius: 55px;
border-bottom-right-radius: 31px;
border-bottom-left-radius: 15px;
}
```

------

所谓的"圆角"其实是这样获得的：

![border-radius](http://olqa2s510.bkt.clouddn.com/border-radius-sh.png)

将一个圆内切于一个直角，再把圆外的部分去掉。我们设置的就是圆的半径。

又或者可以：

将一个椭圆内切于一个直角，再把椭圆外的部分去掉。我们设置的是椭圆的 水平半径 和 垂直半径。

因此，每个角都可以用 `/` 符号拆分成设置 水平半径 和 垂直半径 两项：

```
#test {
border-radius: 11px 22px 33px 44px / 55px 66px 77px 88px;
}
```

等价于：

```
#test {
border-top-left-radius: 11px 55px;
border-top-right-radius: 22px 66px;
border-bottom-right-radius: 33px 77px;
border-bottom-left-radius: 44px 88px;
}
```

## 内径和外径

border-radius内径 = 外径 - 对应的边框宽度。

外径为50px，内径为40px：

```
#test2 {
  border: 10px solid black;
  border-radius: 50px;
}
```

当border-radius半径值小于等于边框宽度时，元素没有内径效果：

外径为50px，没有内径，里面的角都是直角：

```
#test2 {
  border: 50px solid black;
  border-radius: 50px;
}
```

## 特殊图形

### 圆形

元素的宽高相同，且圆角半径为宽高的一半：

```
div {
    width: 100px;
    height: 100px;
    border-radius: 50%;
}
```

### 椭圆：思路和 正圆 一样，仅仅使得宽高不同

```
div {
    width: 120px;
    height: 80px;
    border-radius: 50%;
}
```

### 半圆

```
div {
    width: 100px;
    height: 50px;
    border-radius: 50px 50px 0 0;
}
```

### （直角）扇形

```
div {
    width: 50px;
    height: 50px;
    border-radius: 50px 0 0 0;
}
```


## // 补充说明：

```
div {
    width: 120px;
    height: 80px;
    border-radius: 120px;
}
```

- border-radius可以用具体的px值，也可以用百分比表示，但不能是负数。
  - 如果取值为百分比，水平方向圆角百分比相对于宽度，垂直方向圆角百分比相对于高度
- 如果需要用border-radius重置使得没有圆角：使用none无效，需要取值0
- border-radius对`<img>`没有任何效果