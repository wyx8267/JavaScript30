# 02 - JS and CSS Clock
## 效果需求
在页面上模拟时钟画面，能获取实时时间并且每秒改变一次指针状态。
## 关键要点
1. 时钟指针的旋转效果
2. 获取实时时间
3. 实时改变指针状态
## 步骤分解
1. **CSS部分**调整指针初始位置及旋转轴点。
2. **JS部分**
    1. 用`querySelector`获取三指针的div元素
    2. `new Date()`获取当前时间，`getHours(),getMinutes(),getSeconds()`获取时分秒。
    3. 计算各指针旋转角度
    4. `setInterval()`使指针实时转动
## 基本语法
1. CSS语法：
    1. 旋转角度及旋转轴点
    ```css
    transform: rotate(90deg);
    transform-origin: 100%;
    ```
    2. 回弹效果
    ```css
    transition: all 0.05s;
    transition-timing-function: cubic-bezier(0.01, 1.33, 0.34, 1.3);
    ```
2. `setInterval(fn,delay)`: fn为按计时器执行的函数，delay为间隔时间（或变量）
## 扩展
1. 用伪元素给表盘添加中心点
    ```css
    .clock-face:after{
        width: 2rem;
        height: 2rem;
        left: 50%;
        top: 50%;
        transform: translate(-50%, -50%);
        position: absolute;
        display: block;
        content: '';
        background-color: #fff;
        border-radius: 50%;
        box-shadow: 0 0 0 4px rgba(0, 0, 0, .1),
        inset 0 0 10px rgba(0, 0, 0, .2);
    }
    ```
2. 使指针旋转轴与表盘中心重合

    为每个指针设置`margin-top: -height/2`（指针的宽度在本节中由div的height表现）。
3. deg=90时指针逆时针旋转导致闪烁的解决

    **方法：** 在这个特殊点更改指针的`transition`使该逆时针旋转瞬间完成。
    ```javascript
    if (secondsDegrees === 90) {
        secondHand.style.transition = 'all 0s'
    } else { 
        secondHand.style.transition = 'all 0.05s' 
    }
    ```