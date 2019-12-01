# 01 - JavaScript Drum Kit
## 效果需求
模拟一个打鼓页面，当用户按下ASDFGHJKL这些键时，对应的按钮变大变亮，对应的鼓声响起。
## 关键要点
1. 键盘按下与松开事件
2. 按钮样式改变
3. 播放对应音效
## 步骤分解
1. **添加事件监听**。在window上监听`keydown`键盘事件。
2. **添加触发事件后的处理函数**
    1. 获取键码
    2. 用`querySelector`获取对应音效元素
    3. 用`data-key`获取对应键码元素
    4. 处理音频播放及样式添加
3. **为所有`div.key`添加`transitionend`事件**
    1. 获取所有`.key`元素
    2. 添加事件监听，去除播放样式
## 基本语法
1. **模板字面量**（Template literals）：\`字符串 ${ 变量、属性名 } \`，在字符串中添加变量及变量相关计算的方法。
2. **forEach遍历**：对选取的一组元素进行遍历，为单个元素添加相应事件等
    ```javascript
    const keys = document.querySelectorAll('.key')
    keys.forEach(key => {
        key.addEventListener('transitionend', removeTransition)
    })
    ```
## 难点解决
### 如何实现页面按钮与键盘按键的对应
使用`keydown`事件中的`keyCode`属性，`keyCode`属性值与ASCII码（小写字母）相同
> 可以在[keycode](keycode.info)网站查询

为了给按钮`button`和音效`audio`绑定同一按键，添加了`data-key`属性以存储对应键码，例如按下键盘获取对应键码的音效`audio`标签时:
```javascript
const audio = document.querySelector(`audio[data-key="${e.keyCode}"]`)
```
### 如何实现按住按键不放时，响起连续音效
```javascript
audio.currentTime = 0;
audio.play();
```
每次播放音频前设置播放时间戳为0。
### 如何使页面按键样式恢复
CSS transition动画结束后，会触发`transitionend`事件，利用该事件，在每次样式变化完成后，移除相应样式类。
```javascript
function removeTransition(e) {
    if (e.propertyName !== 'transform') return
    this.classList.remove('playing')
}
```
