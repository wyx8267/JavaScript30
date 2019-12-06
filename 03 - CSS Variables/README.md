# 03 - CSS Variables

## 效果需求

提供三个可变属性选项`spacing, blur, color`，拖动（或改变颜色）会在图片处实时显示对应效果。

## 关键要点

1. 使用CSS variable设置全局变量
2. 获取变化后的样式属性值
3. 使用JS改变CSS全局变量值

## 重点语法

### CSS部分

1. CSS variable

    CSS3新特性，命名写法是`--变量名`，引用时写法是`var(--变量名)`
2. `:root`伪类

    该伪元素匹配的是文档的根元素`<html>`标签。所以用于声明全局的CSS变量。
    ```css
    :root{
        --base: #aaccee;
        --spacing: 10px;
        --blur: 10px;
    }
    img{
        padding: var(--spacing);
        background: var(--base);
        filter: blur(var(--blur));
    }
    ```
3. CSS提供的滤镜`filter`

    CSS 的滤镜提供了一些图形特效，比如高斯模糊、锐化、变色等。它带有一些预设的函数（如下），在使用时加上参数调用这些函数即可。
    ```css
    filter: blur(5px);
    filter: brightness(0.4);
    filter: contrast(200%);
    filter: drop-shadow(16px 16px 20px blue);
    filter: grayscale(50%);
    filter: hue-rotate(90deg);
    filter: invert(75%);
    filter: opacity(25%);
    filter: saturate(30%);
    filter: sepia(60%);
    ```

### JS部分

1. NodeList 和 Array 的区别

    使用`document.querySelectorAll()`时会得到一个NodeList，在 proto 查看它的方法可以发现，其中有` forEach()、item()、keys() `等。而 Array 的 prototype 中有` map()、pop() `等数组才有的方法。

2. HTML5 中的自定义数据属性 dataset

    HTML5 中可以为元素添加非标准的自定义属性，只需加上 data- 前缀，'-'后可以随便添加和命名。添加之后，可以通过元素的 dataset 属性来访问这些值。dataset 的值是 DOMStringMap 的一个实例化对象，其中包含之前所设定的自定义属性的“名-值”对。

    本例中通过`dataset.sizing`获取后缀值
    ```javascript
    const suffix = this.dataset.sizing || '';
    ```
3. 使用JavaScript改变CSS属性值

    JavaScript 中`document.documentElement`即代表文档根元素。
    ```css
    document.documentElement.style.setProperty(`--${this.name}`, this.value + suffix)
    ```
    `style.setProperty(propertyName, value, priority)` 语法:
    - propertyName，被更改的CSS属性。
    - value （可选），新的属性值。如果没有指定, 则当作空字符串。
    - priority （可选），允许设置 "important" CSS 优先级。如果没有指定, 则当作空字符串。