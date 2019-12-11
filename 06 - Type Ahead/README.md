# 06 - Type Ahead
## 效果需求
在输入框中输入任意字母，迅速匹配出含有该字段的城市名或州名，并高亮字段。
## 实现步骤
1. 声明一个空数组，用于存放获取的城市信息。
2. 使用`fetch()`发送HTTP请求获取JSON数据

    1. 获取返回的Promise对象
    2. 解析JSON数据
    3. 存入数组
3. 获取输入框和展示列表元素并添加`change`, `keyup`事件
4. 编写匹配输入字段的函数

    1. 使用`filter()`过滤数组数据
    2. 使用正则表达式构造过滤条件
5. 编写展示匹配结果的函数

    1. 获取要展示的匹配结果数据
    2. 替换需要高亮的字段的样式类
    3. 构造要放入`innerHTML`的内容
    4. 构造内容放入`<ul>`中

## 相关语法
### [Fetch API](https://developer.mozilla.org/zh-CN/docs/Web/API/Fetch_API)

fetch() 必须接受一个参数——资源的路径。无论请求成功与否，它都返回一个 Promise 对象，resolve 对应请求的 Response。

为了获取JSON格式数据，使用 Promise 对象的`then()`方法获取返回的Response，再使用`json()`方法返回一个 Promise，Promise 的解析 resolve 结果是将文本体解析为 JSON。

```javascript
fetch(endpoint)
    .then(blob => blob.json())
    .then(data => cities.push(...data))
```

### ES6的数组扩展语法

展开语法(Spread syntax), 可以在函数调用/数组构造时, 将数组表达式或者string在语法层面展开；还可以在构造字面量对象时, 将对象表达式按key-value的方式展开。