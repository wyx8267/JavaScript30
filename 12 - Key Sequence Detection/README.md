# 12 - Key Sequence Detection

## 实现目标

**验证键盘输入序列是否符合“暗号”**
- 当输入“暗号”（事先定义好的字符串时），从[cornify](https://www.cornify.com)加载一个随机图像到页面上。

## 实现步骤

1. 定义“暗号”字符串
2. 监听并存放输入的字符串
3. 处理输入字符串，当匹配“暗号”时调用cornify

## 功能实现指南

1. 声明存放输入字符的空数组，及暗号字符串。

```javascript
const pressed = [];
const secretCode = 'medosa';
```

2. 监听键盘输入事件

```javascript
window.addEventListener('keyup', (e) => {});
```

3. 以队列形式处理数组，限制数组长度与暗号字符串长度相等，当完整无误地输入暗号字符串时，调用 `cornify_add()` 。

```javascript
window.addEventListener('keyup', (e) => {
  pressed.push(e.key);
  pressed.splice(-secretCode.length - 1, pressed.length - secretCode.length);
  if (pressed.join('') == secretCode) {
    cornify_add();
  }
})
```