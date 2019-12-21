# 08 - Fun with HTML5 Canvas

## 效果需求

1. 使用CANVAS实现一个绘图板
2. 画笔颜色呈彩虹色渐变
3. 画笔粗细呈渐变

## 实现步骤

1. 获取HTML中的`<canvas>`元素，设定宽高为屏幕宽高
2. 使用`getContext('2d')`获取上下文，命名为ctx
3. 设定ctx基本属性：线条及描边颜色、线条宽度、线条末端形状
4. 实现绘画效果：
    1. 设定一个变量作绘画状态标记
    2. 添加鼠标响应监听事件及触发的函数
    3. 设定绘制路径起点和终点
5. 实现彩虹渐变：运用hsl色彩模式的h值的变化
6. 实现粗细渐变：设定画笔粗细范围，超出时进行逆向变化

## 相关语法

### CANVAS

创建绘画环境：
```javascript
const canvas = document.querySelector('#draw')
const ctx = canvas.getContext('2d')
```
设置用于渲染的context:

- `lineCap`：笔触的形状，有 round | butt | square 圆、平、方三种。
- `lineJoin`：线条相较的方式，有 round | bevel | miter 圆交、斜交、斜接三种。
- `lineWidth`：线条的宽度
- `strokeStyle`：线条描边的颜色
- `fillStyle`：填充的颜色

路径绘制方法：

- `beginPath()`：新建一条路径
- `stroke()`：通过线条来绘制图形轮廓
- `moveTo()`：单次绘制操作起点
- `lineTo()`：路径终点

### 彩虹渐变——HSL

HSL色彩模式：

- H(hue) 代表色调，取值为 0~360，专业术语叫色相。
- S 是饱和度，可以理解为掺杂进去的灰度值，取值 0~1。
- L 则是亮度，取值 0~1，或者百分比。

采用绘图时变化H值的方法来变化画笔颜色，可设置当H值超过360时重置为0。

### 画笔粗细渐变

```javascript
ctx.lineWidth = 100;

// in function draw()
if (ctx.lineWidth >= 100 || ctx.lineWidth <= 5) {
    direction = !direction
}
if (direction) {
    ctx.lineWidth ++
} else {
    ctx.lineWidth --
}
```

## 疑难问题

### 未解决：两种设置画笔起始位置的方式造成的不同现象

1. 线条流畅：
```javascript
lastX = e.offsetX
lastY = e.offsetY
```

2. 线条不流畅，有断点：
```javascript
[lastX, lastY] = [e.offsetX, e.offsetY]

// Chrome报错：
// Uncaught TypeError: Cannot set property '0' of undefined "
```
