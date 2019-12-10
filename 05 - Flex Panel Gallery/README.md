# 05 - Flex Panel Gallery
## 效果需求
点击页面图片墙中任一图片，图片会展开，同时从上下两端移入文字。点击已展开的图片后，图片收缩，上下两端文字移出。
## 实现步骤
### CSS
1. 为`.panels`设置`display:flex`。
2. 设定`.panel`的`flex: 1`。
3. 设定`.panel`为`display:flex`（一个元素可以同时为flex-container和flex-item）。设置其flex主轴方向。
4. 设定`.panel`的子元素的文字垂直、水平居中。
5. 设置点击图片后文字移动的样式类。
6. 设置展开图片后的样式类，设定其中的`flex`值。

### JS

1. 获取所有类名为`.panel`的元素。
2. 使用`forEach()`为每个元素添加`click`的事件监听，编写触发事件调用的函数（添加或删除展开图片的样式类）
3. 添加`transitionend`事件监听，编写所调用的函数（添加或删除文字飞入的样式类）
    - 此处使用`if(event.propertyName.includes('flex'))`兼容地识别transitionend中flex变化事件（Safari中事件为`'flex'`，Chrome & FireFox中事件为`'flex-grow'`）
## 相关语法
### Flexbox
本例中使用了三层flex容器嵌套，各自的作用如下：

- `.panels`：使其中的 .panel 按横向的 flex 等分排布（此处为五等分）
- `.panel`：使其中的 `<p>` 按纵向的 flex 等分排布（此处为三等分）
- `p` ：借用 flex 相对于主轴及侧轴的对齐方式，使其中的文字垂直水平居中

> 1. 针对 Flex items 的特性（Children）
>    - flex-growth：伸展值
>    - flex-shrink：可接受的压缩值
>    - flex-basis：元素默认的尺寸值
>    - flex：以上三个值按顺序的缩写
> 2. 针对 Flex container 的特性（Parent）
>    - display: flex：将元素设置成弹性盒子
>    - flex-direction：主轴方向
>    - justify-content：沿主轴的的对齐方式
>    - align-items：沿侧轴的对齐方式
>    - align-content：子元素中文本沿侧轴的对齐方式（只有一行时无效）